---
title: 更改组件的绑定
description: 更改组件的绑定
ms.assetid: 2e59a160-d8d9-4739-a8fa-919760f8eb05
keywords:
- 通知对象 WDK 网络，绑定更改
- 网络通知对象 WDK，绑定更改
- 绑定更改 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c25c990da302101854b146c60b493f6878643ef8
ms.sourcegitcommit: 69939496f6d5cb535aad2bd426ab2baa8d7b9051
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2020
ms.locfileid: "78178060"
---
# <a name="changing-bindings-for-a-component"></a>更改组件的绑定





网络配置子系统始终向通知对象通知有关绑定中影响通知对象的网络组件的更改。 子系统调用 notify 对象的[**INetCfgComponentNotifyBinding：： NotifyBindingPath**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547731(v=vs.85))方法并传递一个值，该值指定更改以及指向更改所涉及的绑定路径的**INetCfgBindingPath**接口的指针。 如果子系统通过了 NCN\_DISABLE 禁用通知对象的网络组件与特定网卡共享的绑定路径，则通知对象可以与另一网卡一起激活绑定，如下面的代码所示。

```C++
HRESULT CSample::NotifyBindingPath(DWORD dwChangeFlag,
        INetCfgBindingPath* pncbp1)
{
    INetCfgComponent *pnccLow;
    INetCfgComponentBindings *pncbind;
    IEnumNetCfgBindingPath *penumncbp;
    INetCfgBindingPath *pncbp2;
    IEnumNetCfgBindingInterface *penumncbi;
    INetCfgBindingInterface *pncbi;
    DWORD dwFlags = EBP_BELOW;
    ULONG celt = 1; // Request one enumeration element. 
    HRESULT hr = S_OK;
    // Retrieve bindings for the notify object's component (m_pncc)
    hr = m_pncc->QueryInterface(IID_INetCfgComponentBindings, 
                                (LPVOID*)&pncbind);
    // Determine if notification is about disabling a binding path.
    if (SUCCEEDED(hr) && (NCN_DISABLE & dwChangeFlag)) {
        // Retrieve enumerator for binding paths for the component.
        hr = pncbind->EnumBindingPaths(dwFlags, &penumncbp);
        // Reset the sequence and retrieve a binding path.
        hr = penumncbp->Reset();
        hr = penumncbp->Next(celt, &pncbp2, NULL);
        // Ensure the binding path is different.
        do {
            if (pncbp1 != pncbp2) break;
   hr = penumncbp->Skip(celt); // skip one element
            hr = penumncbp->Next(celt, &pncbp2, NULL);
        } while (SUCCEEDED(hr));
        if (SUCCEEDED(hr)) {
            // Retrieve enumerator for interfaces of the binding path.
            hr = pncbp2->EnumBindingInterfaces(&penumncbi);
            // Retrieve a binding interface for the binding path.
            hr = penumncbi->Next(celt, &pncbi, NULL);
            // Retrieve the lower network component.
            hr = pncbi->GetLowerComponent(&pnccLow);
            // If the component is a physical network card and binding 
            // is currently disabled, enable binding.
            DWORD dwcc;
            hr = pnccLow->GetCharacteristics(&dwcc);
            if (SUCCEEDED(hr) && (dwcc & NCF_PHYSICAL)) {
                hr = pncbp2->IsEnabled(); // S_FALSE for disabled
                if (hr == S_FALSE)  hr = pncbp2->Enable(TRUE);
            }
        }
        else return hr;
    }
    return hr;
}
```

 

 





