---
title: IServerVirtualDevice::CloseDevice
titlesuffix: SQL Server VDI reference
description: 本文提供 IServerVirtualDevice::CloseDevice 命令的參考。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: 61d877fddb32f6455303a006e8955b1042ce7aa6
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/23/2020
ms.locfileid: "96128902"
---
# <a name="iservervirtualdeviceclosedevice-vdi"></a>IServerVirtualDevice::CloseDevice (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

**CloseDevice** 函式會關閉已使用 IServerVirtualDeviceSet2::OpenDevice 開啟的虛擬裝置

## <a name="syntax"></a>語法

```c
HRESULT IServerVirtualDevice::CloseDevice ();
```

## <a name="return-value"></a>傳回值

|傳回值 | 說明 |
|---|---|
| VD_E_CLOSE | 裝置已關閉。 |
| VD_E_ABORT | 介面處於中止狀態。 |

## <a name="remarks"></a>備註

使用 SignalAbort 來強制執行異常終止之後，不需要 CloseDevice。 如果在使用 SignalAbort 之後叫用 CloseDevice，則不會採取任何動作。

## <a name="next-steps"></a>後續步驟

如需詳細資訊，請參閱 [SQL Server 虛擬裝置介面參考概觀](reference-virtual-device-interface.md)。