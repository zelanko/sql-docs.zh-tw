---
title: IClientVirtualDevice::CompleteCommand
titlesuffix: SQL Server VDI reference
description: 本文提供 IClientVirtualDevice::CompleteCommand 命令的參考。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: dda70978e4daba50018b58c3cf9aeaaaa4374551
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85896941"
---
# <a name="iclientvirtualdevicecompletecommand-vdi"></a>IClientVirtualDevice::CompleteCommand (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

**CompleteCommand** 函式是用來通知 SQL Server 命令已完成。 應該會傳回適用於此命令的完成資訊。

## <a name="syntax"></a>語法

```c
HRESULT IClientVirtualDevice::CompleteCommand (
   VDC_Command*         const pCmd,
   UINT32               dwCompletionCode,
   UINT32               dwBytesTransferred,
   UINT64               dwlPosition
);
```

## <a name="parameters"></a>參數

*pCmd* 這是先前從 IClientVirtualDevice::GetCommand 傳回的命令位址。

*dwCompletionCode* 這是指出完成狀態的 WIN32 狀態碼。 所有命令都必須傳回此參數。 傳回的代碼應該適用於所要執行的命令。 在所有情況下，都會使用 ERROR_SUCCESS 表示已成功執行的命令。 如需可能代碼的完整清單，請參閱 Winerror.h 檔案。 每個命令的一般狀態碼清單會出現在＜命令＞中。

*dwBytesTransferred* 這是已成功傳送的位元組數。 只有資料轉送命令 Read 和 Write 會傳回此值。

*dwlPosition* 這只是 GetPosition 命令的回應。

## <a name="return-value"></a>傳回值

|傳回值 | 說明 |
|---|---|
| NOERROR | 已正確註明完成。 |
| VD_E_INVALID | pCmd 不是使用中的命令。 |
| VD_E_ABORT | 已發出中止信號。 |
| VD_E_PROTOCOL | 裝置未開啟。 |

## <a name="next-steps"></a>後續步驟

如需詳細資訊，請參閱 [SQL Server 虛擬裝置介面參考概觀](reference-virtual-device-interface.md)。
