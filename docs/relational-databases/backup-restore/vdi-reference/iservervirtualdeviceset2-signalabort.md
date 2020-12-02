---
title: IServerVirtualDeviceSet2::SignalAbort
titlesuffix: SQL Server VDI reference
description: 本文提供 IServerVirtualDeviceSet2::SignalAbort 命令的參考。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: 8275d2bbe11b550a804ab9bd9bcf475e1d2fbd34
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/23/2020
ms.locfileid: "96125311"
---
# <a name="iservervirtualdeviceset2signalabort-vdi"></a>IServerVirtualDeviceSet2::SignalAbort (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

**SignalAbort** 函式表明應該發生異常終止。

## <a name="syntax"></a>語法

```c
HRESULT IServerVirtualDeviceSet2::SignalAbort ();
```

## <a name="return-value"></a>傳回值

傳回 *HRESULT* ，指出方法呼叫成功或失敗。 值 NOERROR 表示方法呼叫成功。 非零值則表示已發生錯誤。

## <a name="remarks"></a>備註

伺服器可以隨時選擇中止 BACKUP 或 RESTORE 作業。

此常式會發出所有作業都應該停止的信號。 整體介面會進入中止狀態。 任何裝置上都不會再接受任何命令。 完成代理程式會為每個未完成的要求傳回 ERROR_OPERATION_ABORTED，並返回其呼叫者。 系統會忽略在用戶端記錄的任何完成項。

伺服器可確保不再需要使用從虛擬裝置介面傳回的緩衝區或裝置。 伺服器接著會執行異常終止清除，其中應包含呼叫 IServerVirtualDeviceSet2::Close 函式。

## <a name="next-steps"></a>後續步驟

如需詳細資訊，請參閱 [SQL Server 虛擬裝置介面參考概觀](reference-virtual-device-interface.md)。