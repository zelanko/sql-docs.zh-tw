---
title: IClientVirtualDeviceSet2::SignalAbort
titlesuffix: SQL Server VDI reference
description: 本文提供 IClientVirtualDeviceSet2::SignalAbort 命令的參考。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 0a0d53421f0928b1ebf0ba557afbd29dd8680993
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "70847539"
---
# <a name="iclientvirtualdeviceset2signalabort-vdi"></a>IClientVirtualDeviceSet2::SignalAbort (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**SignalAbort** 函式是用來發出應該發生異常終止的訊號。

## <a name="syntax"></a>語法

```c
HRESULT IClientVirtualDeviceSet2::SignalAbort ();
```

## <a name="return-value"></a>傳回值

傳回 *HRESULT* ，指出方法呼叫成功或失敗。 值 NOERROR 表示方法呼叫成功。 非零值則表示已發生錯誤。

## <a name="remarks"></a>備註

用戶端可以隨時選擇中止 BACKUP 或 RESTORE 作業。 此常式會發出所有作業都應該停止的信號。 整體虛擬裝置集的狀態會進入「中止」狀態。 任何裝置上都不會再傳回任何命令。 所有未完成的命令都會自動完成，並傳回 ERROR_OPERATION_ABORTED 作為完成碼。 用戶端在安全地終止提供給用戶端任何未完成使用的緩衝區之後，應該會呼叫 IClientVirtualDeviceSet2::Close。 如需詳細資訊，請參閱＜異常終止＞。

## <a name="next-steps"></a>後續步驟

如需詳細資訊，請參閱 [SQL Server 虛擬裝置介面參考概觀](reference-virtual-device-interface.md)。