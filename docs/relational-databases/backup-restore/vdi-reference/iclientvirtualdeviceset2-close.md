---
title: IClientVirtualDeviceSet2::Close
titlesuffix: SQL Server VDI reference
description: 本文提供 IClientVirtualDeviceSet2::Close 命令的參考。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 5f87b375773b9c81b29b3b5cac11ea97121c45df
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/10/2019
ms.locfileid: "70847379"
---
# <a name="iclientvirtualdeviceset2close-vdi"></a>IClientVirtualDeviceSet2::Close (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**Close** 函式會關閉 IClientVirtualDeviceSet2::Create 所建立的虛擬裝置集。 這會導致釋放所有與虛擬裝置集相關聯的資源。

## <a name="syntax"></a>語法

```c
HRESULT IClientVirtualDeviceSet2::Close ();
```

## <a name="return-value"></a>傳回值

|傳回值 | 說明 |
|---|---|
| NOERROR | 當虛擬裝置集已成功關閉時，就會傳回此值。 |
| VD_E_PROTOCOL | 因為虛擬裝置集未開啟，所以不會執行任何動作。 |
| VD_E_OPEN | 裝置仍處於開啟狀態。 |

## <a name="remarks"></a>Remarks

叫用 Close 是由用戶端宣告，其應該會釋放虛擬裝置集使用的所有資源。 用戶端必須確保在叫用 Close 之前，所有牽涉到資料緩衝區和虛擬裝置的活動都已終止。 Close 會使得 OpenDevice 傳回的所有虛擬裝置介面都失效。

傳回 Close 呼叫之後，用戶端才能在虛擬裝置集介面上發出 Create 呼叫。 這類呼叫會為後續的 BACKUP 或 RESTORE 作業建立新的虛擬裝置集。

如果在一或多部虛擬裝置仍處於開啟狀態時呼叫 Close，則會傳回 VD_E_OPEN。 在此情況下，會在內部觸發 SignalAbort，確保盡可能適當地關機。 這會釋放 VDI 資源。 用戶端應該等候每部裝置上的 VD_E_CLOSE 指示，再叫用 IClientVirtualDeviceSet2::Close。 如果用戶端知道虛擬裝置集已處於「異常終止」狀態，則不應該預期來自 GetCommand 的 VD_E_CLOSE 指示，且可能會在共用緩衝區上的活動終止時立即叫用 IClientVirtualDeviceSet2::Close。

## <a name="next-steps"></a>後續步驟

如需詳細資訊，請參閱 [SQL Server 虛擬裝置介面參考概觀](reference-virtual-device-interface.md)。