---
title: IClientVirtualDeviceSet2::MapBufferHandle
titlesuffix: SQL Server VDI reference
description: 本文提供 IClientVirtualDeviceSet2::MapBufferHandle 命令的參考。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: 70f6d117fd7a0349f2da2e03ff2603eaf55898fe
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/23/2020
ms.locfileid: "96128963"
---
# <a name="iclientvirtualdeviceset2mapbufferhandle-vdi"></a>IClientVirtualDeviceSet2::MapBufferHandle (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

**MapBufferHandle** 函式是用來從緩衝區控制代碼 (取自其他一些處理序) 取得有效的緩衝區位址。

## <a name="syntax"></a>語法

```c
HRESULT IClientVirtualDeviceSet2::MapBufferHandle (
   DWORD      dwBuffer,
   BYTE**      ppBuffer
);
```

## <a name="parameters"></a>參數

*dwBuffer* 這是 IClientVirtualDeviceSet2::GetBufferHandle 所傳回的控制代碼。

*ppBuffer* 這是在目前處理序中有效的緩衝區位址。

## <a name="return-value"></a>傳回值

|傳回值 | 說明 |
|---|---|
| NOERROR | 此函數已成功。 |
| VD_E_PROTOCOL | 虛擬裝置集目前未開啟。 |
| VD_E_INVALID | ppBuffer 是無效的控制代碼。 |

## <a name="remarks"></a>備註

請務必謹慎，以正確地傳達控制代碼。 控制代碼位於虛擬裝置集的本機。 共用控制代碼的夥伴程序，必須確保緩衝區控制代碼只在原本取得緩衝區的來源虛擬裝置集範圍內使用。

## <a name="next-steps"></a>後續步驟

如需詳細資訊，請參閱 [SQL Server 虛擬裝置介面參考概觀](reference-virtual-device-interface.md)。