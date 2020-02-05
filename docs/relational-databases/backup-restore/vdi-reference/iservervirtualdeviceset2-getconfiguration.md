---
title: IServerVirtualDeviceSet2::GetConfiguration
titlesuffix: SQL Server VDI reference
description: 本文提供 IServerVirtualDeviceSet2::GetConfiguration 命令的參考。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 1d62a2042221bebf04e19a46a21ba81caa7c877b
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "70847249"
---
# <a name="iservervirtualdeviceset2getconfiguration-vdi"></a>IServerVirtualDeviceSet2::GetConfiguration (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**GetConfiguration** 函式會取得用戶端所要求的設定。

## <a name="syntax"></a>語法

```c
HRESULT IServerVirtualDeviceSet2::GetConfiguration (
   VDConfig*   pCfg
);
```

## <a name="parameters"></a>參數

*pCfg* 這是用戶端使用 IClientVirtualDeviceSet2::Create 所指定的設定。

## <a name="return-value"></a>傳回值

傳回 *HRESULT* ，指出方法呼叫成功或失敗。 值 NOERROR 表示方法呼叫成功。 非零值則表示已發生錯誤。

## <a name="remarks"></a>備註

伺服器應該會檢查並回應用戶端所提供的設定。 如需詳細資訊，請參閱＜設定＞。 如果伺服器判斷無法使用提供的設定來正常運作，則可以使用 SignalAbort。

## <a name="next-steps"></a>後續步驟

如需詳細資訊，請參閱 [SQL Server 虛擬裝置介面參考概觀](reference-virtual-device-interface.md)。