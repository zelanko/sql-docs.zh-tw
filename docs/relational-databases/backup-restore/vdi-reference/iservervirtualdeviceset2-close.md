---
title: IServerVirtualDeviceSet2::Close
titlesuffix: SQL Server VDI reference
description: 本文提供 IServerVirtualDeviceSet2::Close 命令的參考。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 2847ef10bd52d69375fa4f13f1d003eb4159961f
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/10/2019
ms.locfileid: "70847469"
---
# <a name="iservervirtualdeviceset2close-vdi"></a>IServerVirtualDeviceSet2::Close (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**Close** 函式會關閉 IServerVirtualDeviceSet2::Open 所開啟的虛擬裝置集。 這會導致釋放所有與虛擬裝置建立關聯的資源。 在此函式傳回之後，IServerVirtualDeviceSet2 控制代碼沒什麼用處，應該將其傳回到 COM。

## <a name="syntax"></a>語法

```c
HRESULT IServerVirtualDeviceSet2::Close ();
```

## <a name="return-value"></a>傳回值

|傳回值 | 說明 |
|---|---|
| VD_E_PROTOCOL | 裝置仍處於開啟狀態。 |

## <a name="remarks"></a>Remarks

在關閉裝置之前，不應執行關閉虛擬裝置集。 如果發生這種情況，則會傳回 VD_E_PROTOCOL。 此動作會導致 Close 立即釋放其共用記憶體的對應。 如果伺服器持續預期從虛擬裝置介面傳回的資源擁有權，則會受到存取違規的影響。 此介面會執行 SignalAbort 處理。

執行完成代理程式時，會先完成所有未處理完畢的命令，再回到其呼叫端。 任何未處理完畢的命令都會以 ERROR_OPERATION_ABORTED 來完成。 也就是說，會為每個這類命令叫用回呼函式。

在所有情況下，包括傳回錯誤時，Close 都會釋放虛擬裝置介面的所有資源。 從 VDI 傳回的任何緩衝區和其他介面指標都會變成無效。

在卸載 COM 程式庫之前，請務必確定已終止完成代理程式。 如果在完成代理程式回到其呼叫端之前卸載程式庫，則此處理序可能會導致指令違規。

## <a name="next-steps"></a>後續步驟

如需詳細資訊，請參閱 [SQL Server 虛擬裝置介面參考概觀](reference-virtual-device-interface.md)。