---
title: IServerVirtualDeviceSet2::FreeBuffer
titlesuffix: SQL Server VDI reference
description: 本文提供 IServerVirtualDeviceSet2::FreeBuffer 命令的參考。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: d75d859b4340e95d705037b603f186871acb3b42
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/23/2020
ms.locfileid: "96125344"
---
# <a name="iservervirtualdeviceset2freebuffer-vdi"></a>IServerVirtualDeviceSet2::FreeBuffer (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

**FreeBuffer** 函式會從虛擬裝置集取得共用記憶體緩衝區。

## <a name="syntax"></a>語法

```c
HRESULT IServerVirtualDeviceSet2::FreeBuffer (
   LPVOID   pBuffer,
   UINT32   dwSize
);
```

## <a name="parameters"></a>參數

*pBuffer* 這會傳回 IServerVirtualDeviceSet2::AllocateBuffer 所傳回的緩衝區。

*dwSize* 這是緩衝區的大小 (以位元組為單位)。 這不包含用戶端要求的任何前置詞區域。 伺服器會隱藏任何這類區域，且在傳回緩衝區位址之前，會有可用的空間。

## <a name="return-value"></a>傳回值

|傳回值 | 說明 |
|---|---|
| NOERROR | 會傳回緩衝區。 |
| VD_E_INVALID | 參數無效。 |

## <a name="next-steps"></a>後續步驟

如需詳細資訊，請參閱 [SQL Server 虛擬裝置介面參考概觀](reference-virtual-device-interface.md)。