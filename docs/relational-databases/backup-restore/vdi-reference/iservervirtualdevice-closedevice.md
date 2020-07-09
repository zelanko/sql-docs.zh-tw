---
title: IServerVirtualDevice::CloseDevice
titlesuffix: SQL Server VDI reference
description: 本文提供 IServerVirtualDevice::CloseDevice 命令的參考。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 3e9ff54c500b626d667622105a39e742c5e2a339
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85896836"
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