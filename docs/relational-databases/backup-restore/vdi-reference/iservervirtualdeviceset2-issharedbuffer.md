---
title: IServerVirtualDeviceSet2::IsSharedBuffer
titlesuffix: SQL Server VDI reference
description: 本文提供 IServerVirtualDeviceSet2::IsSharedBuffer 命令的參考。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: cd3e7abfd1d250a170e0de4ebc1b392bc5857468
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "70847359"
---
# <a name="iservervirtualdeviceset2issharedbuffer-vdi"></a>IServerVirtualDeviceSet2::IsSharedBuffer (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**IsSharedBuffer** 函式會判斷指定的緩衝區位址是否參考 AllocateBuffer 方法所提供其中一個共用緩衝區。

## <a name="syntax"></a>語法

```c
HRESULT IServerVirtualDeviceSet2::IsSharedBuffer (
   LPVOID   lpBuffer
);
```

## <a name="parameters"></a>參數

*lpBuffer* 這是緩衝區的位址。

## <a name="return-value"></a>傳回值

|傳回值 | 說明 |
|---|---|
| TRUE | 緩衝區是共用緩衝區。 |
| FALSE | 緩衝區不是虛擬裝置集的一部分。 |

## <a name="next-steps"></a>後續步驟

如需詳細資訊，請參閱 [SQL Server 虛擬裝置介面參考概觀](reference-virtual-device-interface.md)。