---
title: OID_GEN_VENDOR_DRIVER_VERSION
description: 为查询，OID_GEN_VENDOR_DRIVER_VERSION OID 指定微型端口驱动程序的供应商分配版本号。
ms.assetid: 37CB6A21-9AF2-49BF-AFBA-868C0C6C5383
keywords:
- OID_GEN_VENDOR_DRIVER_VERSION
ms.date: 11/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e69adabe84a2320f4e9e28209b7d7e64817d0cf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387865"
---
# <a name="oidgenvendordriverversion"></a>OID_GEN_VENDOR_DRIVER_VERSION

为查询，OID_GEN_VENDOR_DRIVER_VERSION OID 指定微型端口驱动程序的供应商分配版本号。

不支持组的请求。

## <a name="remarks"></a>备注

返回值的低位部分指定的次版本;高序位后半部分指定的主版本。

此 OID 是必需的 NDIS 6.0 和更高版本的微型端口驱动程序。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| Version | Windows Vista 及更高版本 |
| Header | Ntddndis.h （包括 Ndis.h） |

