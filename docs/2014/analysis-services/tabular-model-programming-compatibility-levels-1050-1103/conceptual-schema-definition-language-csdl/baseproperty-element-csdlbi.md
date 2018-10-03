---
title: BaseProperty 元素 (CSDLBI) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: d0f63e52-7330-4b2c-a929-7a517acc6921
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3dcea67deac28838f190947c0b890b86537536c4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48198808"
---
# <a name="baseproperty-element-csdlbi"></a>BaseProperty 元素 (CSDLBI)
  BaseProperty 元素為複雜類型，可做為其他元素的基底。  
  
 其屬性可以出現在資料行和量值中。  
  
## <a name="elements-and-attributes"></a>元素和屬性  
 下表列出定義 BaseProperty 元素的元素和屬性。  
  
|名稱|是否必要|描述|  
|----------|-----------------|-----------------|  
|Alignment|否|成員 (資料行、量值、導覽屬性、階層或層級) 的名稱，藉由實作 Member 類型所定義。|  
|FormatString|否|成員的顯示名稱。|  
|IsRightToLeft|否|布林值，指出欄位是否包含可由右至左讀取的文字。<br /><br /> 如果省略此屬性，則會使用 (模型的) 預設設定。|  
|SortDirection|否|值，指出一般的欄位值排序方式。 此屬性的內容是由 SortDirection 簡單類型定義。<br /><br /> 如果省略此屬性，排序方向是依據欄位的資料類型指派。|  
|單位|否|套用至欄位值以表示單位的符號。<br /><br /> 如果省略，則單位為未知。|  
  
## <a name="alignment-element"></a>Alignment 元素  
 此簡單類型會定義用於區分成員的命名格式。  
  
|值|描述|  
|-----------|-----------------|  
|None|使用屬性名稱。|  
|內容|使用內送關聯性名稱。|  
|合併式|根據目前文法的規則，串連內送關聯性名稱和屬性名稱。|  
  
## <a name="sortdirection-element"></a>SortDirection 元素  
 此簡單類型會定義用於區分成員的命名格式。  
  
|值|描述|  
|-----------|-----------------|  
|None|使用屬性名稱。|  
|內容|使用內送關聯性名稱。|  
|合併式|串連內送關聯性名稱和屬性名稱。|  
  
## <a name="see-also"></a>另請參閱  
 [了解表格式物件模型](../representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
  
