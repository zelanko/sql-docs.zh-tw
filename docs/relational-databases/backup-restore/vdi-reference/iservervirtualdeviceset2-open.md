---
title: IServerVirtualDeviceSet2::Open
titlesuffix: SQL Server VDI reference
description: 本文提供 IServerVirtualDeviceSet2::Open 命令的參考。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 552394db26a1b236a4d6997f6dbfba77d12086ee
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/10/2019
ms.locfileid: "70847219"
---
# <a name="iservervirtualdeviceset2open-vdi"></a>IServerVirtualDeviceSet2::Open (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**Open** 函式會在伺服器上開啟虛擬裝置集，且它必須是使用 COM 所提供介面控制代碼進行的第一次呼叫。

## <a name="syntax"></a>語法

```c
HRESULT IServerVirtualDeviceSet2::Open (
   LPCWSTR      lpInstanceName,
   LPCWSTR      lpName
);
```

## <a name="parameters"></a>參數

*lpInstanceName* 這個字串會識別 SQL 命令傳送目標的 SQL Server 實例。 可以傳遞 Null 來識別目前電腦上的預設實例。

*lpName* 這是由 BACKUP 或 RESTORE 命令的第一個 VIRTUAL_DEVICE= 子句所提供。 此名稱可作為索引鍵，以存取用戶端所建立的虛擬裝置集。

## <a name="return-value"></a>傳回值

|傳回值 | 說明 |
|---|---|
| NOERROR | 此函數已成功。 |
| VD_E_INVALID | 所提供名稱未識別可供伺服器存取的虛擬裝置集。 |

## <a name="remarks"></a>Remarks

成功叫用此函式之後，伺服器可能會使用 GetConfiguration 和 SetConfiguration 繼續設定虛擬裝置集。

## <a name="next-steps"></a>後續步驟

如需詳細資訊，請參閱 [SQL Server 虛擬裝置介面參考概觀](reference-virtual-device-interface.md)。