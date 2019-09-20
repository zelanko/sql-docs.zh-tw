---
title: IServerVirtualDeviceSet2::RequestBuffers
titlesuffix: SQL Server VDI reference
description: 本文提供 IServerVirtualDeviceSet2::RequestBuffers 命令的參考。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 1b941f251c9093f10abbced8c3522f1719a1580e
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/10/2019
ms.locfileid: "70847179"
---
# <a name="iservervirtualdeviceset2requestbuffers-vdi"></a>IServerVirtualDeviceSet2::RequestBuffers (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**RequestBuffers** 函式會通知 VDI，伺服器將需要特定數量且具有指定大小和對齊方式需求的緩衝區。

## <a name="syntax"></a>語法

```c
HRESULT IServerVirtualDeviceSet2::RequestBuffers (
   DWORD   dwSize,
   DWORD   dwAlignment,
   DWORD   dwCount
);
```

## <a name="parameters"></a>參數

*dwSize* 識別每個緩衝區的大小。 此大小應該只包含資料所需的區域。 VDI 會負責任何對齊方式和前置詞的需求。

*dwAlignment* 這些緩衝區所需的對齊方式。 可以使用比 'BeginConfiguration' 所指定基本對齊值更嚴格的值。 如果值為 0，則會預設為基本對齊值。

*dwCount* 'AllocateBuffer' 所要求且具有指定大小和對齊方式的緩衝區數目。

## <a name="return-value"></a>傳回值

|傳回值 | 說明 |
|---|---|
| NOERROR | 此函數已成功。 |
| VD_E_ABORT | 已要求中止。 |
| VD_E_PROTOCOL | 此集合不是處於可宣告緩衝區配置的狀態 (請參閱狀態轉換矩陣)。 |
| VD_E_MEMORY | 無法取得所要求的記憶體。 |

## <a name="remarks"></a>Remarks

在使用 AllocateBuffer 配置緩衝區之前，應該使用這個方法。 具有指定大小和對齊方式的緩衝區集合會使用 RequestBuffers 進行要求，然後使用 AllocateBuffer 配置個別的緩衝區。

在設定階段期間，RequestBuffers 呼叫會「加總」一起，以便於 EndConfiguration 呼叫時可以使用單一緩衝區 (在那時進行配置)。 完成設定之後，任何 RequestBuffers 呼叫都會導致立即配置更多的緩衝區空間。

## <a name="next-steps"></a>後續步驟

如需詳細資訊，請參閱 [SQL Server 虛擬裝置介面參考概觀](reference-virtual-device-interface.md)。