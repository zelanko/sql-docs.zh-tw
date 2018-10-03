---
title: Member 元素 (CSDLBI) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: 1ba225f5-3867-4aae-a519-e3c277688d1e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f193cb746b8df43c33aa65ea3d69d87ab7c36655
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48218828"
---
# <a name="member-element-csdlbi"></a>Member 元素 (CSDLBI)
  Member 元素為複雜類型，可做為其他元素的基底。  
  
 其屬性 (Attribute) 可以出現在資料行、量值、導覽屬性 (Property)、階層和層級中。  
  
## <a name="elements-and-attributes"></a>元素和屬性  
 下表列出定義 Member 元素的元素和屬性。  
  
|名稱|是否必要|描述|  
|----------|-----------------|-----------------|  
|名稱||成員 (資料行、量值、導覽屬性、階層或層級) 的名稱，藉由實作 TMember 類型所定義。|  
|Caption|是|成員的顯示名稱。|  
|ContextualNameRule|是|用於區分成員的命名格式。 此屬性的內容是由 ContextualNameRule 簡單類型定義。|  
|Hidden||布林值，指出是否對用戶端隱藏成員。<br /><br /> 預設值為 false，表示在用戶端中可以看見資料行。|  
|ReferenceName||用於在 DAX 查詢中參考成員的識別碼。 如果省略此屬性，則會使用欄位名稱|  
  
## <a name="contextualnamerule-element"></a>ContextualNameRule 元素  
 此簡單類型會定義用於區分成員的命名格式。  
  
|值|描述|  
|-----------|-----------------|  
|None|使用屬性名稱。|  
|內容|使用內送關聯性名稱。|  
|合併式|串連內送關聯性名稱和屬性名稱。|  
  
## <a name="see-also"></a>另請參閱  
 [了解表格式物件模型](../representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
  
