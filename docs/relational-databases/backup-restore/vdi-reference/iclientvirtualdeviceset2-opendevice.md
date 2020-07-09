---
title: IClientVirtualDeviceSet2::OpenDevice
titlesuffix: SQL Server VDI reference
description: 本文提供 IClientVirtualDeviceSet2::OpenDevice 命令的參考。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: f28a7547d16a03e5be963b3cfeb837e7ab78c007
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85896874"
---
# <a name="iclientvirtualdeviceset2opendevice-vdi"></a>IClientVirtualDeviceSet2::OpenDevice (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

**OpenDevice** 函式會開啟虛擬裝置集的其中一部裝置。

## <a name="syntax"></a>語法

```c
HRESULT IClientVirtualDeviceSet2::OpenDevice (
   LPCWSTR                  lpName,
   IClientVirtualDevice**   ppVirtualDevice

);
```

## <a name="parameters"></a>參數

*lpName* 這會識別虛擬裝置。

*ppVirtualDevice* 當函式成功時，會傳回虛擬裝置的介面指標。 此介面用於 GetCommand 和 CompleteCommand。

## <a name="return-value"></a>傳回值

|傳回值 | 說明 |
|---|---|
| NOERROR | 此函數已成功。 |
| VD_E_ABORT | 已要求中止。 |
| VD_E_OPEN |所有裝置都已開啟。 |
| VD_E_PROTOCOL | 集合未處於初始化狀態，或此特定裝置已開啟。 |
| VD_E_INVALID | 裝置名稱無效。 這不是組成集合的其中一個已知名稱。 |

## <a name="remarks"></a>備註

可能會傳回 VD_E_OPEN 且未發生問題。 用戶端可能會透過迴圈呼叫 OpenDevice，直到傳回此代碼為止。
如果已設定多部裝置 (例如 n 部裝置)，虛擬裝置集會傳回 n 個唯一的裝置介面。 第一個裝置的名稱與虛擬裝置集相同。 其他裝置會以 BACKUP/RESTORE 陳述式的 VIRTUAL_DEVICE 子句所指定的名稱來命名。

您可以使用 GetConfiguration 函式等到裝置可開啟為止。

如果此函數不成功，會透過 ppVirtualDevice 傳回 Null 值。

## <a name="next-steps"></a>後續步驟

如需詳細資訊，請參閱 [SQL Server 虛擬裝置介面參考概觀](reference-virtual-device-interface.md)。