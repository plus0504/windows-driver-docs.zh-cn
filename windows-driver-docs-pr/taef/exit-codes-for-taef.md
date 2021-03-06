---
title: TAEF 的退出代码
description: TAEF 的退出代码
ms.assetid: DEA060FE-317F-47fe-8934-22F7AF879F1C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b8196027a4fe08dfa472b1a1ea7d0afe870fa25
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378093"
---
# <a name="exit-codes-for-taef"></a>TAEF 的退出代码


如果在执行期间出现错误，则"Te.exe"命令行可执行文件为 TAEF 前端返回非零退出代码。 有不同的方式可能会出现错误，然后在进程退出代码反映。

从 Te.exe 在进程退出代码是一个 32 位数字，并在该数内的不同位反映不同类型的错误。 退出代码细分，如下所示：

-   位 0 到 15:"测试结果值"-这是未通过测试数。
-   16 23 位："TestMode 结果值"-TestMode （尚不支持使用） 中的错误。
-   24 30 位："工具结果值"-工具本身中的错误。

最高有效位 （位 31，有符号的数字符号位） 不用于避免有符号/无符号的混淆。 始终在进程退出代码为正。 实际上声明的详细信息：

-   如果退出代码为小于或等于 0xFFFF (65535)，则它是数字的非传递 （failed、 blocked、 运行，或跳过） 该 Te.exe 执行测试。 如果更该 65535 测试未通过，然后将值上限为 65535。
-   如果退出代码值大于 0xFFFF/65535 出现了问题以外，在执行时测试代码。

以下列表显示当前"工具结果值"和它们的解释。

| 工具结果值 | Te.exe 退出代码       | 解释                                                                                            |
|----------------------|------------------------|-----------------------------------------------------------------------------------------------------------|
| 1                    | 0x01000000 (16777216)  | 帮助请求 （"/？" 或"/ ！")-未执行测试。                                               |
| 2                    | 0x02000000 (33554432)  | Wex.Logger 报告了错误。                                                                             |
| 3                    | 0x03000000 (50331648)  | 无法初始化 Wex.Logger。                                                                       |
| 4                    | 0x04000000 (67108864)  | 生成的 Wex.Logger 无效通过/失败计数 （通常不平衡的 StartGroup/Engroup 调用从测试） |
| 5                    | 0x05000000 (83886080)  | 无效的命令行 (未指定任何有效的测试文件，"/ inproc"具有多个测试文件指定)。  |
| 6                    | 0x06000000 (100663296) | 发生某些其他异常。                                                                            |
| 7                    | 0x07000000 (117440512) | 未执行测试。                                                                                   |
| 8                    | 0x08000000 (134217728) | TAEF 会话已超时。                                                                                   |
| 9                    | 0x09000000 (150994944) | 请求的版本信息 ("/ 版本")-未执行测试。                                  |

 

 

 





