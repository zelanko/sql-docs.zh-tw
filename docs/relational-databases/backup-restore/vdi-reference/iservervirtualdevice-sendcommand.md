---
title: IServerVirtualDevice::SendCommand
titlesuffix: SQL Server VDI reference
description: 本文提供 IServerVirtualDevice::SendCommand 命令的參考。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: f03e87863d21abfc4abf91811616cbacd14caff2
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/23/2020
ms.locfileid: "96125379"
---
# <a name="iservervirtualdevicesendcommand-vdi"></a>IServerVirtualDevice::SendCommand (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

**SendCommand** 函式會使用從 IServerVirtualDeviceSet2::OpenDevice 傳回的虛擬裝置物件，將命令傳送給用戶端。

## <a name="syntax"></a>語法

```c
HRESULT IServerVirtualDevice::SendCommand (
   VDS_Command*   pCmd
);
```

## <a name="parameters"></a>參數

*pCmd* 這是命令要求區塊的指標。 如需詳細資訊，請參閱＜命令＞。 completionFunction 欄位必須設定為指向具有下列簽章的函式位址：

```c
void callbackFunction ( VDS_Command *pCmd);
```

當用戶端指出已完成命令時，完成代理程式就會發出此回呼。 SQL Server 會設定 pCmd 的 completionContext 欄位。 其目的是要為回呼函式提供內容。

## <a name="return-value"></a>傳回值

|傳回值 | 說明 |
|---|---|
| NOERROR | 命令已成功排入用戶端佇列。 |
| VD_E_QUEUE_FULL | 裝置佇列已滿。 |
| VD_E_IO_ERROR | 裝置處於 IO-ERROR 狀態。 |
| VD_E_PROTOCOL | 裝置不在作用中。 |

## <a name="remarks"></a>備註

嘗試傳送命令但發生錯誤時，會叫用回呼函式，並將命令緩衝區中的 completionCode 設定如下：

| completionCode | 錯誤 |
|---|---|
| VD_E_QUEUE_FULL | ERROR_NO_SYSTEM_RESOURCES |
| VD_E_IO_ERROR   | ERROR_IO_DEVICE |
| VD_E_PROTOCOL   | ERROR_INVALID_HANDLE |
| VD_E_ABORT      | ERROR_OPERATION_ABORTED |

## <a name="next-steps"></a>後續步驟

如需詳細資訊，請參閱 [SQL Server 虛擬裝置介面參考概觀](reference-virtual-device-interface.md)。