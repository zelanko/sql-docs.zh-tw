---
title: "Member 元素 (CSDLBI) |Microsoft 文件"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 1ba225f5-3867-4aae-a519-e3c277688d1e
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7bc33ebc0cd970c58f4f27d4b49a972c9ed724c0
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="member-element-csdlbi"></a>Member 元素 (CSDLBI)
  Member 元素為複雜類型，可做為其他元素的基底。  
  
 其屬性 (Attribute) 可以出現在資料行、量值、導覽屬性 (Property)、階層和層級中。  
  
## <a name="elements-and-attributes"></a>元素和屬性  
 下表列出定義 Member 元素的元素和屬性。  
  
|名稱|是否必要|說明|  
|----------|-----------------|-----------------|  
|名稱||成員 (資料行、量值、導覽屬性、階層或層級) 的名稱，藉由實作 TMember 類型所定義。|  
|Caption|是|成員的顯示名稱。|  
|ContextualNameRule|是|用於區分成員的命名格式。 此屬性的內容是由 ContextualNameRule 簡單類型定義。|  
|Hidden||布林值，指出是否對用戶端隱藏成員。<br /><br /> 預設值為 false，表示在用戶端中可以看見資料行。|  
|ReferenceName||用於在 DAX 查詢中參考成員的識別碼。 如果省略此屬性，則會使用欄位名稱|  
  
## <a name="contextualnamerule-element"></a>ContextualNameRule 元素  
 此簡單類型會定義用於區分成員的命名格式。  
  
|Value|說明|  
|-----------|-----------------|  
|無|使用屬性名稱。|  
|內容|使用內送關聯性名稱。|  
|合併式|串連內送關聯性名稱和屬性名稱。|  
  
## <a name="see-also"></a>另請參閱  
 [了解表格式物件模型在相容性層級 1050年透過 1103](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
  

