---
title: IClientVirtualDeviceSet2::OpenInSecondaryEx
titlesuffix: SQL Server VDI reference
description: 本文提供 IClientVirtualDeviceSet2::OpenInSecondaryEx 命令的參考。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: e674061244eb5e4a03717e8b3030c89412792e2b
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85896866"
---
# <a name="iclientvirtualdeviceset2openinsecondaryex-vdi"></a>IClientVirtualDeviceSet2::OpenInSecondaryEx (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

**OpenInSecondaryEx** 函式會開啟次要用戶端中的虛擬裝置集。 主要用戶端必須已使用 CreateEx 和 GetConfiguration 來設定虛擬裝置集。

## <a name="syntax"></a>語法

```c
HRESULT IClientVirtualDeviceSet2::OpenInSecondaryEx (
   LPCWSTR      lpInstanceName,
   LPCWSTR      lpSetName
);
```

## <a name="parameters"></a>參數

*lpInstanceName* 這個字串會識別 SQL 命令傳送目標的 SQL Server 實例。

*lpSetName* 這會識別集合。 此名稱會區分大小寫，且必須符合主要用戶端在叫用 IClientVirtualDeviceSet2::Create 時所使用的名稱。

## <a name="return-value"></a>傳回值

|傳回值 | 說明 |
|---|---|
| NOERROR | 此函數已成功。 |
| VD_E_PROTOCOL | 虛擬裝置集尚未開啟，或虛擬裝置集尚未準備好接受來自次要用戶端的開啟要求。 |
| VD_E_ABORT | 作業即將中止。 |

## <a name="remarks"></a>備註

使用多個處理序模型時，主要用戶端會負責偵測次要用戶端的正常和異常終止。

實例名稱必須識別 T-SQL 發出目標的實例。 Null 可識別預設實例。 不接受 "machineName\" 前置詞。

OpenInSecondaryEx 會取代原始 SQL Server 7.0 版介面中所定義的原始 IClientVirtualDeviceSet::OpenInSecondary。 新的開發應該使用 OpenInSecondaryEx。

## <a name="next-steps"></a>後續步驟

如需詳細資訊，請參閱 [SQL Server 虛擬裝置介面參考概觀](reference-virtual-device-interface.md)。