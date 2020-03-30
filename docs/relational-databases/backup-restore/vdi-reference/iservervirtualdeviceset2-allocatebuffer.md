---
title: IServerVirtualDeviceSet2::AllocateBuffer
titlesuffix: SQL Server VDI reference
description: 本文提供 IServerVirtualDeviceSet2::AllocateBuffer 命令的參考。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 8c28009fae8b52264b541ca3eb4281ab9abccf63
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "70847489"
---
# <a name="iservervirtualdeviceset2allocatebuffer-vdi"></a>IServerVirtualDeviceSet2::AllocateBuffer (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**AllocateBuffer** 函式會從虛擬裝置集取得共用記憶體緩衝區。

## <a name="syntax"></a>語法

```c
HRESULT IServerVirtualDeviceSet2::AllocateBuffer (
   LPVOID*      ppBuffer,
   UINT32      dwSize,
   UINT32      dwAlignment
);
```

## <a name="parameters"></a>參數

*ppBuffer* 這會傳回緩衝區開頭的指標。

*dwSize* 這是緩衝區的大小 (以位元組為單位)。 這不包含用戶端要求的任何前置詞區域。 伺服器會隱藏任何這類區域，且在傳回緩衝區位址之前，會有可用的空間。

*dwAlignment* 這會指定緩衝區的對齊界限。 例如，值 4096 會確保緩衝區在 4096 位元組的界限上對齊。 這表示傳回的位址會將低序位 12 位元設為零。 這個參數必須是 2 的乘冪。

## <a name="return-value"></a>傳回值

|傳回值 | 說明 |
|---|---|
| NOERROR | 會傳回緩衝區。 |
| VD_E_MEMORY | 發生記憶體不足的狀況。 |
| VD_E_INVALID | 參數無效。 |

## <a name="next-steps"></a>後續步驟

如需詳細資訊，請參閱 [SQL Server 虛擬裝置介面參考概觀](reference-virtual-device-interface.md)。