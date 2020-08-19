---
description: ADCPROP_AUTORECALC_ENUM
title: ADCPROP_AUTORECALC_ENUM |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADCPROP_AUTORECALC_ENUM
helpviewer_keywords:
- ADCPROP_AUTORECALC_ENUM [ADO]
ms.assetid: ded4f087-87b9-4efa-8026-bde53d3e9e8a
author: rothja
ms.author: jroth
ms.openlocfilehash: e0b9cf745ae30d11d85aeba1c916594e09392c6d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88451610"
---
# <a name="adcprop_autorecalc_enum"></a>ADCPROP_AUTORECALC_ENUM
指定當 [MSDataShape](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) 提供者在階層式記錄集中重新計算匯總和計算資料行時。  
  
 這些常數只會與 **MSDataShape** 提供者和 **記錄集** 「**自動**重新計算」動態屬性搭配使用，而此屬性是在 [ADO 動態屬性索引](../../../ado/reference/ado-api/ado-dynamic-property-index.md) 中參考，並記載于適用于 OLE DB 檔的 [OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) 或 [microsoft 資料成形服務的 microsoft 資料成形服務](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) 中。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adRecalcAlways**|1|預設值。 每當 **MSDataShape** 提供者判斷匯出資料行所依存的值是否已變更時，就會重新計算。|  
|**adRecalcUpFront**|0|只有在一開始建立階層式 **記錄集**時才會計算。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 這些常數沒有 ADO/WFC 對等專案。
