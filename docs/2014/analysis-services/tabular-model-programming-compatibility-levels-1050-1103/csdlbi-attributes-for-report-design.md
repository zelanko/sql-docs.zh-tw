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
ms.openlocfilehash: ee53cb3e4910e988403350bac5c993ef68b5170d
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84940124"
---
# <a name="csdlbi-attributes-for-report-design"></a>報表設計的 CSDLBI 屬性
  本節描述表格式模型化的 CSDL 延伸模組中影響 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 查詢設計的屬性。  
  
## <a name="model-attributes"></a>模型屬性  
 這些屬性是在 CSDL [EntityContainer](https://msdn.microsoft.com/library/bb399169.aspx)元素的子項目上定義的。  
  
|屬性名稱|資料類型|描述|  
|--------------------|---------------|-----------------|  
|文化特性|Text|表示用於貨幣格式的文化特性。 如果省略，則使用 EN-US。|  
|IsRightToLeft|Boolean|表示文字欄位值預設是否應該由右至左讀取|  
  
## <a name="entity-attributes"></a>實體屬性  
 這些屬性是在 CSDL EntitySet 或 EntityType 元素的子元素上定義的。  
  
|屬性名稱|資料類型|描述|  
|--------------------|---------------|-----------------|  
|`ReferenceName`|Text|用於在 DAX 查詢中參考此實體的識別碼。 如果省略，則使用名稱。|  
|`Caption`|Text|實體的顯示名稱。|  
|`Documentation`|Text|協助商務使用者了解資料意義的描述性文字。|  
|`Hidden`|Boolean|表示是否應顯示實體。 預設值為 `false`。|  
|`CollectionCaption`|Text|用於參考實體的一組執行個體的複數名稱。 如果省略，則使用 Caption 屬性。|  
|`DisplayKey`|MemberRef[]|用於對商務使用者識別實體執行個體的已排序的欄位清單。 參考可以包含執行個體屬性和導覽屬性。 在參考導覽屬性時，會顯示目標實體的 `DisplayKey`。 如果省略 `DisplayKey` 值，則使用 Key 欄位。|  
|`DefaultImage`|MemberRef|欄位的參考，這個欄位包含用於向商務使用者以視覺方式識別實體執行個體的影像。 如果省略，則使用實體中的第一個影像欄位 (如果有)。|  
|`DefaultDetails`|MemberRef[]|已排序的欄位清單，這些欄位表示向商務使用者顯示有關實體執行個體、預設的一組詳細資訊。如果省略，則使用實體中的前五 (5) 個欄位，但不包括 `Key`、`DisplayKey` 或 `DefaultImage` 所參考的那些欄位。|  
|`SortProperties`|MemberRef[]|已排序的欄位清單，這些欄位通常是實體執行個體排序依據。 在這些欄位上排序時，會使用每個欄位上指定的 `SortDirection`。 如果省略，則使用 `DisplayKey` 欄位|  
|`DefaultMeasure`|MemberRef|模型中定義之量值的參考，或具有預設彙總函式之數值欄位的參考，以表示該量值或欄位應該做為實體的多個執行個體的預設表示。 如果省略，則使用實體執行個體的計數。|  
|`DefaultLocation`|MemberRef|欄位的參考，欄位值表示與實體執行個體相關聯的預設位置。 如果省略，則使用實體中的第一個位置欄位 (如果有)。|  
  
## <a name="field-attributes"></a>欄位屬性  
 這些屬性是在 CSDL 屬性或[NavigationProperty](https://msdn.microsoft.com/library/bb387104.aspx)元素的子項目上定義的。  
  
|屬性名稱|資料類型|描述|  
|--------------------|---------------|-----------------|  
|`ReferenceName`|Text|用於在 DAX 查詢中參考此實體的識別碼。 如果省略，則使用欄位名稱。|  
|`Caption`|Text|實體的顯示名稱。 如果省略，則 `ReferenceName` 會使用欄位的。|  
|`Documentation`|Text|協助商務使用者了解欄位意義的描述性文字。|  
|`Hidden`|Boolean|表示是否應顯示欄位。 預設值為 `false`，表示會顯示欄位。|  
|`DisplayFolder`|Text|在其中顯示此欄位的資料夾的名稱 (完整路徑)。 如果省略，則在模型根中顯示欄位。|  
|`ContextualNameRule`|列舉|值，表示是否應該根據使用內容來修改屬性名稱及其修改方式。 可能的值為：`None`、`Role`、`Merge`。|  
|`Alignment`|列舉|值，表示在表格式簡報中對齊欄位值的方式。 可能的值為 `Default`、`Center`、`Left`、`Right`。 如果省略，預設值會根據欄位的資料類型決定對齊方式。|  
|`FormatString`|Text|.NET 格式字串，指出欄位的值應該如何根據預設格式化。 如果省略，則採用下列格式：<br /><br /> -Datetime 欄位：地區簡短日期或 "d"<br />-具有預設彙總函式的浮點欄位和整數位段：區域號碼或 "n"<br />-沒有預設彙總函式的整數：區域十進位數或 "d"<br /><br /> 如果是所有其他類型的欄位，則不套用任何格式字串。|  
|`Units`|Text|套用至欄位值以表示單位的符號。 如果省略，則假設單位為未知。|  
|`Width`|整數|慣用的寬度（以字元為單位），應保留以在表格式呈現中顯示欄位的值。 如果省略，則預設寬度是以欄位的資料類型為基礎。|  
|`SortDirection`|列舉|值，表示一般的欄位值排序方式。 可能的值為 `Default`、`Ascending`、`Descending`。 如果省略，預設值會根據欄位的資料類型來指派排序方向。|  
|`IsRightToLeft`|Boolean|表示欄位是否包含應該由右至左讀取的文字。 如果省略，則採用模型設定。|  
|`OrderBy`|MemberRef|模型中另一個欄位的參考，可定義此欄位值的排序次序。 這兩個欄位的值必須具有 1:1 對應，否則排序行為是未定義的。 如果省略，欄位就會根據自己的值來排序。|  
|`Contents`|列舉|列舉，描述欄位的子類型或內容。 如果省略，則不會假設任何特定的子類型，除非欄位的資料類型是 Binary，在此情況下會採用影像。 如需支援的內容類型完整清單，請參閱 AMO 文件集。|  
|`DefaultAggregateFunction`|列舉|值，表示通常用於彙總此欄位的預設函數 (如果有)。 可能的值為 `None`、`Sum`、`Average`、`Count`、`Min`、`Max`。 如果省略，對於數值欄位採用 `Sum`，對於所有其他欄位則採用 `None`。|  
|`IsSimpleMeasure`|Boolean|表示量值是否只是數值欄位的簡單彙總。 這類彙總可以視需要在查詢中輕鬆地定義，因此應該從模型定義中省略以提高效能。 如果省略，則假設為 `false`。|  
|`Kpi`<br /><br /> `KpiGoal`<br /><br /> `KpiStatus`|Subelement|表示量值元素要做為 KPI。 KPI 子元素使用 KpiGoal 和 KpiStauts 元素以定義相關的顯示影像和目標範圍。|  
  
  
