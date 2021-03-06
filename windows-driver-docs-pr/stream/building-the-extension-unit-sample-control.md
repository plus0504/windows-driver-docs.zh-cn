---
title: 生成扩展单元示例控件
description: 生成扩展单元示例控件
ms.assetid: 57dd0bc3-2aab-42a2-b0c5-7f6ecaefd300
keywords:
- 扩展单元控制 WDK USB 视频类
- 控件 WDK USB 视频类
ms.date: 01/30/2019
ms.localizationpriority: medium
ms.openlocfilehash: 522a9e5a433ec8c079212207954c9e45454f52ce
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370382"
---
# <a name="building-the-extension-unit-sample-control"></a>生成扩展单元示例控件

您可以编译此部分创建 UVC 扩展单元示例控件中的代码。 生成此项目时，您创建可以使用与相应的应用程序来获取和设置属性扩展单元上的 Microsoft ActiveX 控件。

若要使用该控件，您需要实现特定的扩展单元功能的硬件。 或者，可以使用一个 USB 仿真程序。

使用以下步骤来生成控件：

1. 安装以下包：

    - Microsoft Windows Server 2003 Service Pack 1 (SP1) 驱动程序开发工具包 (DDK)
    - Microsoft DirectX 9.0 SDK 更新 (2005 年 2 月)
    - Microsoft DirectX 9.0 2005 年 2 月 SDK 其他功能

2. 将从以下主题的示例代码复制到单独的文件。

    [UVC 扩展单位的示例接口](sample-interface-for-uvc-extension-units.md)

    [示例扩展单元插件 DLL](sample-extension-unit-plug-in-dll.md)

    [UVC 扩展单位的示例注册表项](sample-registry-entry-for-uvc-extension-units.md)

    [UVC 扩展单位的示例应用程序](sample-application-for-uvc-extension-units.md)

    [支持扩展单位的自动更新事件](supporting-autoupdate-events-with-extension-units.md)

    [提供 UVC INF 文件](providing-a-uvc-inf-file.md)

3. 创建*源*文件，如下所示：

    ```cpp
    TARGETNAME= uvcxuplgn
    TARGETTYPE= DYNLINK
    TARGETPATH= obj
    TARGETEXT=  ax

    DLLENTRY=_DllMainCRTStartup
    DLLBASE=0x10080000
    USE_MSVCRT=1

    USE_STATIC_ATL=1

    USER_INCLUDES= $(O)

    INCLUDES=

    SOURCES= interface.idl \
     uvcxuplgn.cpp \
             stdafx.cpp    \
             interface_i.c \
             vidcap_i.c    \
             xuproxy.cpp

    TARGETLIBS= \
            $(SDK_LIB_PATH)\kernel32.lib          \
            $(SDK_LIB_PATH)\user32.lib            \
            $(SDK_LIB_PATH)\gdi32.lib             \
            $(SDK_LIB_PATH)\advapi32.lib          \
            $(SDK_LIB_PATH)\comdlg32.lib          \
            $(SDK_LIB_PATH)\ole32.lib             \
            $(SDK_LIB_PATH)\oleaut32.lib          \
            $(SDK_LIB_PATH)\uuid.lib              \
            $(SDK_LIB_PATH)\comctl32.lib
    ```

4. 创建*生成文件*文件，如下所示：

    ```cpp
    #############################################################################
    #
    #       Copyright (C) Microsoft Corporation 1995
    #       All Rights Reserved.
    #
    #       MAKEFILE for WDM device driver kit
    #
    #############################################################################

    #
    # DO NOT EDIT THIS FILE!!!  Edit .\sources. if you want to add a new source
    # file to this component.  This file merely indirects to the real make file
    # that is shared by all the driver components of the Windows NT DDK
    #

    !if "$(WIN2K_DDKBUILD)" == ""
    !INCLUDE $(NTMAKEENV)\makefile.def
    !endif
    ```

5. 使用*Guidgen.exe*工具 （Microsoft Windows SDK 中包含） 创建三个 Guid:

    - 第一个 GUID 用作扩展单元的属性组 ID。 基于 x 的 GUID 占位符替换为在新的 GUID *Xuproxy.h、 Xusample.rgs,Xuplgin.inf，* 和你在硬件级别的扩展单元描述符中。
    - 用作 IID 的第二个 GUID 扩展单元。 Y 基于 GUID 占位符替换为在新的 GUID *Interface.idl*并*Xuplgin.inf*。
    - 第三个 GUID 用作扩展单元的类 GUID (clsid)。 Z 基于 GUID 占位符替换为在新的 GUID *Xuplgin.inf、 Xuproxy.h*，和*Xusample.rgs。*

6. 复制*Extend.def*从 WIA 扩展示例和对其进行编辑。 *Uvcxuplugn.def*应包含：

    ```cpp
    LIBRARY uvcxuplgn

    EXPORTS
        DllGetClassObject   PRIVATE
        DllCanUnloadNow     PRIVATE
        DllRegisterServer   PRIVATE
        DllUnregisterServer PRIVATE
    ```

7. 创建*Uvcxuplgn.cpp* ，如下所示：

    ```cpp
    #include "stdafx.h"
    CComModule _Module;
    #include <initguid.h>
    #include "interface.h"
    #include "xuproxy.h"
    BEGIN_OBJECT_MAP(ObjectMap)
    OBJECT_ENTRY(CLSID_ExtensionUnit, CExtension)
    END_OBJECT_MAP()

    STDAPI DllRegisterServer(void)
    {
        return _Module.RegisterServer(FALSE, NULL);
    }

    STDAPI DllUnregisterServer(void)
    {
        return _Module.UnregisterServer();
    }

    EXTERN_C
    BOOL
    DllMain(
        HINSTANCE   hinst,
        DWORD       dwReason,
        LPVOID      lpReserved)
    {
        switch (dwReason) {
            case DLL_PROCESS_ATTACH:

                _Module.Init (ObjectMap, hinst);
                break;

            case DLL_PROCESS_DETACH:
                _Module.Term();
                break;
        }
        return TRUE;
    }

    extern "C" STDMETHODIMP DllCanUnloadNow(void)
    {
        return _Module.GetLockCount()==0 ? S_OK : S_FALSE;
    }

    extern "C" STDAPI DllGetClassObject(
        REFCLSID    rclsid,
        REFIID      riid,
        LPVOID      *ppv)
    {
        return _Module.GetClassObject(rclsid, riid, ppv);
    }
    ```

8. 创建*Stdafx.h* ，如下所示：

    ```cpp
    // stdafx.h : include file for standard system include files,
    //      or project specific include files that are used frequently,
    //      but are changed infrequently

    #if !defined(AFX_STDAFX_H__722DC775_FE6F_42FB_BED5_E1E299976D17__INCLUDED_)
    #define AFX_STDAFX_H__722DC775_FE6F_42FB_BED5_E1E299976D17__INCLUDED_

    #if _MSC_VER > 1000
    #pragma once
    #endif // _MSC_VER > 1000

    #define STRICT
    #ifndef _WIN32_WINNT
    #define _WIN32_WINNT 0x0400
    #endif
    #define _ATL_APARTMENT_THREADED

    #include <atlbase.h>
    //You may derive a class from CComModule and use it if you want to override
    //something, but do not change the name of _Module
    extern CComModule _Module;
    #include <atlcom.h>
    #include <atlctl.h>

    //{{AFX_INSERT_LOCATION}}
    // Microsoft Visual C++ will insert additional declarations immediately before the previous line.

    #endif // !defined(AFX_STDAFX_H__722DC775_FE6F_42FB_BED5_E1E299976D17__INCLUDED)
    ```

9. 创建*Stdafx.cpp* ，如下所示：

    ```cpp
    // stdafx.cpp : source file that includes just the standard includes
    //  stdafx.pch will be the pre-compiled header
    //  stdafx.obj will contain the pre-compiled type information

    #include "stdafx.h"

    #ifdef _ATL_STATIC_REGISTRY
    #include <statreg.h>
    #include <statreg.cpp>
    #endif

    #include <atlimpl.cpp>
    ```

10. 通过调用生成 cZg WDK 构建环境中生成该示例。
