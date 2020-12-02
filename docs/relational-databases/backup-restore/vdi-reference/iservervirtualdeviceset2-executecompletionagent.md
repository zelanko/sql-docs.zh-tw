---
title: IServerVirtualDeviceSet2::ExecuteCompletionAgent
titlesuffix: SQL Server VDI reference
description: 本文提供 IServerVirtualDeviceSet2::ExecuteCompletionAgent 命令的參考。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: ce53793d624c0a56fda48805c5c2fc8fc178e42c
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/23/2020
ms.locfileid: "96128880"
---
# <a name="iservervirtualdeviceset2executecompletionagent-vdi"></a>IServerVirtualDeviceSet2::ExecuteCompletionAgent (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

**ExecuteCompletionAgent** 函式是用來實作完成代理程式的主要迴圈。

## <a name="syntax"></a>語法

```c
HRESULT IServerVirtualDeviceSet2::ExecuteCompletionAgent ();
```

## <a name="return-value"></a>傳回值

傳回 *HRESULT* ，指出方法呼叫成功或失敗。 值 NOERROR 表示方法呼叫成功。 非零值則表示已發生錯誤。

## <a name="remarks"></a>備註

完成代理程式會提供一項機制，SQL Server 可以透過該機制將其本身與虛擬裝置命令完成同步。 它必須是作用中，才能發出任何命令，且應該在所有裝置都關閉之前保持作用中狀態。

由於 SQL Server 可能需要執行特殊的執行緒初始化，因此此介面不會啟動新的控制項執行緒。 相反地，SQL Server 會設定執行緒，然後將控制項傳遞給這個常式。 此執行緒在 Windows NT 處理序間通訊 (IPC) 機制上必須為可封鎖，且能夠呼叫透過 IServerVirtualDevice::SendCommand 傳送之命令所提供的任何回呼函式。

此函式在叫用 IServerVirtualDeviceSet2::Close or SignalAbort 之前不會傳回。

## <a name="next-steps"></a>後續步驟

如需詳細資訊，請參閱 [SQL Server 虛擬裝置介面參考概觀](reference-virtual-device-interface.md)。