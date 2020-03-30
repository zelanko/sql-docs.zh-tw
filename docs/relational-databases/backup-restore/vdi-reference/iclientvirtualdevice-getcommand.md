---
title: IClientVirtualDevice::GetCommand
titlesuffix: SQL Server VDI reference
description: 本文提供 IClientVirtualDevice::GetCommand 命令的參考。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: a861377924b4bb3cc1c1d2a4b83eba660fbf99e0
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "70847589"
---
# <a name="iclientvirtualdevicegetcommand-vdi"></a>IClientVirtualDevice::GetCommand (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**GetCommand** 函式是用來取得下一個排入裝置佇列的命令。 要求時，此函數會等候下一個命令。

## <a name="syntax"></a>語法

```c
HRESULT IClientVirtualDevice::GetCommand (
   DWORD               dwTimeOut,
   VDC_Command**      const ppCmd
);
```

## <a name="parameters"></a>參數

*ppCmd* 成功傳回命令時，參數會傳回所要執行命令的位址。 傳回的記憶體是唯讀的。 當命令完成時，此指標會傳遞至 CompleteCommand 常式。 如需每個命令的詳細資訊，請參閱＜命令＞。

*dwTimeOut* 這是等候時間 (以毫秒為單位)。 使用 INFINTE 可永遠等候。 使用 0 可輪詢是否有命令。 如果目前沒有可用的命令，則會傳回 VD_E_TIMEOUT。 如果發生逾時，用戶端會決定下一個動作。

## <a name="return-value"></a>傳回值

|傳回值 | 說明 |
|---|---|
| NOERROR | 已擷取命令。 |
| VD_E_CLOSE | 伺服器已關閉裝置。 |
| VD_E_TIMEOUT | 沒有命令可用並發生逾時。 |
| VD_E_ABORT | 用戶端或伺服器已使用 SignalAbort 強制關閉。 |

## <a name="remarks"></a>備註

傳回 VD_E_CLOSE 時，SQL Server 已關閉裝置。 這是正常關機的一部分。 關閉所有裝置之後，用戶端會叫用 IClientVirtualDeviceSet2::Close，以關閉虛擬裝置集。

當此常式必須封鎖以等候命令時，執行緒會保留在「可警示」條件中。

## <a name="next-steps"></a>後續步驟

如需詳細資訊，請參閱 [SQL Server 虛擬裝置介面參考概觀](reference-virtual-device-interface.md)。