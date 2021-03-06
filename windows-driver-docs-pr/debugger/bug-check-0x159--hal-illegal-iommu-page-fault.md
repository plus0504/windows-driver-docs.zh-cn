---
title: Bug 检查 0x159 HAL_ILLEGAL_IOMMU_PAGE_FAULT
description: HAL_ILLEGAL_IOMMU_PAGE_FAULT bug 检查具有 0x00000159 值。
ms.assetid: 2431EDC4-53B3-4E17-86D8-3B6911B21C98
keywords:
- Bug 检查 0x159 HAL_ILLEGAL_IOMMU_PAGE_FAULT
- HAL_ILLEGAL_IOMMU_PAGE_FAULT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- HAL_ILLEGAL_IOMMU_PAGE_FAULT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 205a130063e804f91179758b12e432d72fd798f0
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67520030"
---
# <a name="bug-check-0x159-halillegaliommupagefault"></a>Bug 检查 0x159：HAL\_非法\_IOMMU\_页面\_容错


HAL\_非法\_IOMMU\_页面\_故障错误检查的值为 0x00000159。 这表示 IOMMU 已传递对正在释放 ASID 页面错误。 该驱动程序是负责完成任何即时请求之前的时间和此检测错误中此点指示系统中的驱动程序没有这样做。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。


## <a name="halillegaliommupagefault-parameters"></a>HAL\_非法\_IOMMU\_页面\_错误参数


| 参数 | 描述                       |
|-----------|-----------------------------------|
| 1         | IOMMU 供应商消除二义性       |
| 2         | 指向错误数据包           |
| 3         | 供应商特定错误数据包数据 |
| 4         | 供应商特定错误数据包数据 |

 

| 参数 | 描述                           |
|-----------|---------------------------------------|
| 1         | IOMMU 供应商消除二义性 = 0x3xxx。 |
| 2         | 状态                                |
| 3         | PASID                                 |
| 4         | DirectoryBase                         |

 

 

 




