---
Description: The WpdHelloWorldDriver Sample
title: WpdHelloWorldDriver 示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c180f73c536bc0f40d2553e22665016de754a3b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524854"
---
# <a name="the-wpdhelloworlddriver-sample"></a>WpdHelloWorldDriver 示例


示例驱动程序支持四个对象： 一个设备对象、 存储对象、 一个文件夹和文件对象。 每个对象支持相应的属性。 在文件中定义了这些属性*WpdObjectProperties.h*。

示例驱动程序支持显示十个只读属性的设备对象。 下表中列出了这些属性，其类型和它们的值。

| 属性名                     | 属性类型 | 值                              |
|-----------------------------------|---------------|------------------------------------|
| 设备\_协议                  | 字符串        | "Hello World 协议验证 1.00"    |
| 设备\_固件\_版本         | 字符串        | "1.0.0.0"                          |
| DEVICE\_POWER\_LEVEL              | 整型       | 100                                |
| 设备\_模型                     | 字符串        | "Hello World ！"                     |
| 设备\_制造商              | 字符串        | "Windows 便携式设备组"   |
| 设备\_友好                  | 字符串        | "Hello World ！"                     |
| DEVICE\_SERIAL\_NUMBER            | 字符串        | "01234567890123-45676890123456"    |
| 设备\_支持\_NONCONSUMABLE   | Bool          | True                               |
| WPD\_DEVICE\_TYPE                 | 整型       | WPD\_DEVICE\_TYPE\_GENERIC         |
| WPD\_功能\_对象\_类别 | GUID          | WPD\_功能\_类别\_存储 |

 

该驱动程序支持的存储对象，显示六个只读属性。 下表中列出了这些属性，其类型和它们的值。

| 属性名                     | 属性类型  | 值                              |
|-----------------------------------|----------------|------------------------------------|
| 存储\_容量                 | 64 位整数 | 1024 \* 1024                       |
| 存储\_免费\_空间\_IN\_字节   | 64 位整数 | （与上面相同）                    |
| 存储\_串行\_数           | 字符串         | 98765432109876-54321098765432      |
| 存储\_文件\_系统\_类型       | 字符串         | FAT32                              |
| 存储\_说明              | 字符串         | 世界您好！ 内存存储系统 |
| WPD\_存储\_类型                | 整型        | WPD\_STORAGE\_TYPE\_FIXED\_ROM     |
| WPD\_功能\_对象\_类别 | GUID           | WPD\_功能\_类别\_存储 |

 

该驱动程序支持公开三个只读属性的文件夹对象。 下表中列出了这些属性，其类型和它们的值。

| 属性名                            | 属性类型 | 值              |
|------------------------------------------|---------------|--------------------|
| WPD\_对象\_日期\_已修改              | 日期          | 2006/6/26 5:0:0.0  |
| WPD\_对象\_日期\_已创建               | 日期          | 2006/1/25 12:0:0.0 |
| WPD\_OBJECT\_ORIGINAL\_FILE\_NAME\_VALUE | 字符串        | 文档          |

 

该驱动程序支持的文件对象来公开三个只读属性。 下表中列出了这些属性，其类型和它们的值。

| 属性名                     | 属性类型 | 值              |
|-----------------------------------|---------------|--------------------|
| WPD\_对象\_日期\_已修改       | 日期          | 2006/6/26 5:0:0.0  |
| WPD\_对象\_日期\_已创建        | 日期          | 2006/1/25 12:0:0.0 |
| WPD\_对象\_原始\_文件\_名称 | 字符串        | Readme.txt         |

 

除了上述属性 （例如，设备、 存储、 文件夹或文件） 的每个对象还支持七个常见的 WPD 对象属性。 这些是大多数情况下包含特定于对象的值的只读属性。 下表中列出了这些属性，其类型和它们的值。

|                                     |               |                 |
|-------------------------------------|---------------|-----------------|
| 属性名                       | 属性类型 | 值           |
| WPD\_对象\_ID                     | 字符串        | 特定于的对象 |
| WPD\_OBJECT\_PERSISTENT\_UNIQUE\_ID | 字符串        | 特定于的对象 |
| WPD\_对象\_父\_ID             | 字符串        | 特定于的对象 |
| WPD\_对象\_名称                   | 字符串        | 特定于的对象 |
| WPD\_对象\_格式                 | GUID          | 特定于的对象 |
| WPD\_对象\_内容\_类型          | GUID          | 特定于的对象 |
| WPD\_OBJECT\_CAN\_DELETE            | Bool          | False           |

 

 

 



