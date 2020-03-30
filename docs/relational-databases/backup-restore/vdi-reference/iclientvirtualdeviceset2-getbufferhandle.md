---
title: IClientVirtualDeviceSet2::GetBufferHandle
titlesuffix: SQL Server VDI reference
description: 本文提供 IClientVirtualDeviceSet2::GetBufferHandle 命令的參考。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 844ddad21eaf3fb579d6a0981f2a042238e92372
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "70847329"
---
# <a name="iclientvirtualdeviceset2getbufferhandle-vdi"></a>IClientVirtualDeviceSet2::GetBufferHandle (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

某些應用程式可能需要多個處理序，才能在 **IClientVirtualDevice2::GetCommand** 所傳回的緩衝區上運作。 在此情況下，接收命令之處理序可以使用 **GetBufferHandle** 取得處理序的獨立控制代碼來識別緩衝區。 接著可以將此控制代碼傳達給也會開啟相同虛擬裝置集的其他處理序。 該處理序接著會使用 IClientVirtualDeviceSet2::MapBufferHandle，取得緩衝區的位址。 此位址可能是與其夥伴不同的位址，因為每個程序可能會對應到不同位址的緩衝區。

## <a name="syntax"></a>語法

```c
HRESULT IClientVirtualDeviceSet2::GetBufferHandle (
   BYTE*         pBuffer,
   DWORD*      pBufferHandle
);
```

## <a name="parameters"></a>參數

*pBuffer* 這是從 Read 或 Write 命令取得的緩衝區位址。

*pBufferHandle* 會傳回緩衝區的唯一識別碼。

## <a name="return-value"></a>傳回值

|傳回值 | 說明 |
|---|---|
| NOERROR | 此函數已成功。 |
| VD_E_PROTOCOL | 虛擬裝置集目前未開啟。 |
| VD_E_INVALID | pBuffer 不是有效的位址。 |

## <a name="remarks"></a>備註

叫用 GetBufferHandle 函式的處理序會負責在資料轉送完成時叫用 IClientVirtualDevice2::CompleteCommand。

## <a name="next-steps"></a>後續步驟

如需詳細資訊，請參閱 [SQL Server 虛擬裝置介面參考概觀](reference-virtual-device-interface.md)。