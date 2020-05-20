---
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
ms.openlocfilehash: 7b00d507a2ddbe596311e16d51a302f4b0dc0dc5
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760714"
---
# <a name="adcprop_autorecalc_enum"></a>ADCPROP_AUTORECALC_ENUM
指定[MSDataShape](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)提供者在階層式記錄集中重新計算匯總和計算結果欄的時機。  
  
 這些常數僅適用于**MSDataShape**提供者和**記錄集**「**自動**重新計算」動態屬性，這會在[ADO 動態屬性索引](../../../ado/reference/ado-api/ado-dynamic-property-index.md)中參考，並記載于適用于[OLE DB 的 Microsoft 資料指標服務](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)，以及 OLE DB 檔的[microsoft 資料成形服務](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adRecalcAlways**|1|預設值。 每當**MSDataShape**提供者判斷計算結果欄所依賴的值已變更時重新計算。|  
|**adRecalcUpFront**|0|只有在一開始建立階層式**記錄集**時才會計算。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等  
 這些常數沒有 ADO/WFC 對應項。
