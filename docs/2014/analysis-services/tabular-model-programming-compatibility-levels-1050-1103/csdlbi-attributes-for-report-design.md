---
title: 報表設計的 CSDLBI 屬性 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
ms.assetid: 61ba3a27-790e-43bc-b421-e01bf2fdbda6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b7d2a9f075879ce1bfa0c0e7257ea8a2495562c0
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "60157845"
---
# <a name="csdlbi-attributes-for-report-design"></a>報表設計的 CSDLBI 屬性
  本節描述表格式模型化的 CSDL 延伸模組中影響 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 查詢設計的屬性。  
  
## <a name="model-attributes"></a>模型屬性  
 這些屬性定義在 csdl 的子元素上[EntityContainer](https://msdn.microsoft.com/library/bb399169.aspx)項目。  
  
|屬性名稱|資料類型|描述|  
|--------------------|---------------|-----------------|  
|Culture|文字|表示用於貨幣格式的文化特性。 如果省略，則使用 EN-US。|  
|IsRightToLeft|布林|表示文字欄位值預設是否應該由右至左讀取|  
  
## <a name="entity-attributes"></a>實體屬性  
 這些屬性是在 CSDL EntitySet 或 EntityType 元素的子元素上定義的。  
  
|屬性名稱|資料類型|描述|  
|--------------------|---------------|-----------------|  
|`ReferenceName`|文字|用於在 DAX 查詢中參考此實體的識別碼。 如果省略，則使用名稱。|  
|`Caption`|文字|實體的顯示名稱。|  
|`Documentation`|文字|協助商務使用者了解資料意義的描述性文字。|  
|`Hidden`|布林|表示是否應顯示實體。 預設為 `false`。|  
|`CollectionCaption`|文字|用於參考實體的一組執行個體的複數名稱。 如果省略，則使用 Caption 屬性。|  
|`DisplayKey`|MemberRef[]|用於對商務使用者識別實體執行個體的已排序的欄位清單。 參考可以包含執行個體屬性和導覽屬性。 在參考導覽屬性時，會顯示目標實體的 `DisplayKey`。 如果省略 `DisplayKey` 值，則使用 Key 欄位。|  
|`DefaultImage`|MemberRef|欄位的參考，這個欄位包含用於向商務使用者以視覺方式識別實體執行個體的影像。 如果省略，則使用實體中的第一個影像欄位 (如果有)。|  
|`DefaultDetails`|MemberRef[]|已排序的欄位清單，這些欄位表示向商務使用者顯示有關實體執行個體、預設的一組詳細資訊。如果省略，則使用實體中的前五 (5) 個欄位，但不包括 `Key`、`DisplayKey` 或 `DefaultImage` 所參考的那些欄位。|  
|`SortProperties`|MemberRef[]|已排序的欄位清單，這些欄位通常是實體執行個體排序依據。 在這些欄位上排序時，會使用每個欄位上指定的 `SortDirection`。 如果省略，則使用 `DisplayKey` 欄位|  
|`DefaultMeasure`|MemberRef|模型中定義之量值的參考，或具有預設彙總函式之數值欄位的參考，以表示該量值或欄位應該做為實體的多個執行個體的預設表示。 如果省略，則使用實體執行個體的計數。|  
|`DefaultLocation`|MemberRef|欄位的參考，欄位值表示與實體執行個體相關聯的預設位置。 如果省略，則使用實體中的第一個位置欄位 (如果有)。|  
  
## <a name="field-attributes"></a>欄位屬性  
 這些屬性定義在 CSDL 屬性的子元素或[NavigationProperty](https://msdn.microsoft.com/library/bb387104.aspx)項目。  
  
|屬性名稱|資料類型|描述|  
|--------------------|---------------|-----------------|  
|`ReferenceName`|文字|用於在 DAX 查詢中參考此實體的識別碼。 如果省略，則使用欄位名稱。|  
|`Caption`|文字|實體的顯示名稱。 如果省略，欄位的`ReferenceName`用。|  
|`Documentation`|文字|協助商務使用者了解欄位意義的描述性文字。|  
|`Hidden`|布林|表示是否應顯示欄位。 預設值為 `false`，表示會顯示欄位。|  
|`DisplayFolder`|文字|在其中顯示此欄位的資料夾的名稱 (完整路徑)。 如果省略，則在模型根中顯示欄位。|  
|`ContextualNameRule`|Enum|值，表示是否應該根據使用內容來修改屬性名稱及其修改方式。 可能的值為：`None`、`Role`、`Merge`。|  
|`Alignment`|Enum|值，表示在表格式簡報中對齊欄位值的方式。 可能的值為 `Default`、`Center`、`Left`、`Right`。 如果省略，預設值會決定根據欄位的資料類型的對齊方式。|  
|`FormatString`|文字|.NET 格式字串，表示如何格式化該欄位的值預設。 如果省略，則採用下列格式：<br /><br /> 日期時間欄位： 地區的簡短日期或"d"<br />-浮點數的欄位和整數欄位，預設值彙總函式： 區域數字或"n"<br />為沒有預設值整數彙總函式： 區域的十進位數字或"d"<br /><br /> 如果是所有其他類型的欄位，則不套用任何格式字串。|  
|`Units`|文字|套用至欄位值以表示單位的符號。 如果省略，則假設單位為未知。|  
|`Width`|Integer|慣用的寬度，以在表格式簡報中顯示欄位的值應該保留的字元。 如果省略，預設寬度根據欄位的資料類型。|  
|`SortDirection`|Enum|值，表示一般的欄位值排序方式。 可能的值為 `Default`、`Ascending`、`Descending`。 如果省略，預設值，指派排序方向會根據欄位的資料類型。|  
|`IsRightToLeft`|布林|表示欄位是否包含應該由右至左讀取的文字。 如果省略，則採用模型設定。|  
|`OrderBy`|MemberRef|在此模型會定義此欄位的值的排序次序內的另一個欄位的參考。 這兩個欄位的值必須具有 1:1 對應，否則排序行為是未定義的。 如果省略，欄位就會根據自己的值來排序。|  
|`Contents`|Enum|列舉，描述欄位的子類型或內容。 如果省略，沒有特定的子類型會假設，除非該欄位的資料類型為 Binary，在此情況下則假設使用 Image。 如需支援的內容類型完整清單，請參閱 AMO 文件集。|  
|`DefaultAggregateFunction`|Enum|值，表示通常用於彙總此欄位的預設函數 (如果有)。 可能的值為 `None`、`Sum`、`Average`、`Count`、`Min`、`Max`。 如果省略，對於數值欄位採用 `Sum`，對於所有其他欄位則採用 `None`。|  
|`IsSimpleMeasure`|布林|表示量值是否只是數值欄位的簡單彙總。 這類彙總可以視需要在查詢中輕鬆地定義，因此應該從模型定義中省略以提高效能。 如果省略，則假設為 `false`。|  
|`Kpi`<br /><br /> `KpiGoal`<br /><br /> `KpiStatus`|Subelement|表示量值元素要做為 KPI。 KPI 子元素使用 KpiGoal 和 KpiStauts 元素以定義相關的顯示影像和目標範圍。|  
  
  
