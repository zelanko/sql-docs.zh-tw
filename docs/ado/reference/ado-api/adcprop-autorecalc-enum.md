---
title: ADCPROP_AUTORECALC_ENUM | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c3c085a09b800bb5dd6ce02ca3fa2d570b74190e
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66718576"
---
# <a name="adcpropautorecalcenum"></a>ADCPROP_AUTORECALC_ENUM
指定何時[MSDataShape](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)提供者重新計算彙總與導出資料行中的階層式資料錄集。  
  
 這些常數僅能搭配**MSDataShape**提供者並**資料錄集**」**自動重新計算**"中參考的動態屬性[ADO動態屬性索引](../../../ado/reference/ado-api/ado-dynamic-property-index.md)中並加以說明[OLE DB 的 Microsoft 資料指標服務](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)或是[Microsoft Data Shaping Service 的 OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)文件。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adRecalcAlways**|1|預設值。 每當重新計算**MSDataShape**提供者會決定取決於導出資料行的值已變更。|  
|**adRecalcUpFront**|0|開始建立階層時，才會計算**資料錄集**。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 這些常數不需要 ADO/WFC 對等項目。
