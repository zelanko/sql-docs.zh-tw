---
title: "報表設計的 CSDLBI 屬性 |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 61ba3a27-790e-43bc-b421-e01bf2fdbda6
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d0adb4ce534d0e70a309bf99b6e6a16479c931f3
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="csdlbi-attributes-for-report-design"></a>報表設計的 CSDLBI 屬性

[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

  本節描述表格式模型化的 CSDL 延伸模組中影響 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 查詢設計的屬性。  
  
## <a name="model-attributes"></a>模型屬性  
 這些屬性在 csdl 的子元素上定義[EntityContainer](http://msdn.microsoft.com/library/bb399169.aspx)項目。  
  
|屬性名稱|資料類型|Description|  
|--------------------|---------------|-----------------|  
|Culture|Text|表示用於貨幣格式的文化特性。 如果省略，則使用 EN-US。|  
|IsRightToLeft|布林|表示文字欄位值預設是否應該由右至左讀取|  
  
## <a name="entity-attributes"></a>實體屬性  
 這些屬性是在 CSDL EntitySet 或 EntityType 元素的子元素上定義的。  
  
|屬性名稱|資料類型|Description|  
|--------------------|---------------|-----------------|  
|**ReferenceName**|Text|用於在 DAX 查詢中參考此實體的識別碼。 如果省略，則使用名稱。|  
|**Caption**|Text|實體的顯示名稱。|  
|**文件集**|Text|協助商務使用者了解資料意義的描述性文字。|  
|**Hidden**|布林|表示是否應顯示實體。 預設值為 **false**。|  
|**CollectionCaption**|Text|用於參考實體的一組執行個體的複數名稱。 如果省略，則使用 Caption 屬性。|  
|**DisplayKey**|MemberRef[]|用於對商務使用者識別實體執行個體的已排序的欄位清單。 參考可以包含執行個體屬性和導覽屬性。 在參考導覽屬性時**DisplayKey**目標的實體隨即出現。 如果**DisplayKey**省略值，則使用 Key 欄位。|  
|**DefaultImage**|MemberRef|欄位的參考，這個欄位包含用於向商務使用者以視覺方式識別實體執行個體的影像。 如果省略，則使用實體中的第一個影像欄位 (如果有)。|  
|**DefaultDetails**|MemberRef[]|代表預設欄位的已排序的清單設定的實體執行個體的相關商務使用者顯示的詳細資訊。如果省略，第一次五 （5） 實體中使用欄位時，不包括已由參考這些**金鑰**， **DisplayKey**，或**DefaultImage**。|  
|**SortProperties**|MemberRef[]|已排序的欄位清單，這些欄位通常是實體執行個體排序依據。 這些欄位上排序時**SortDirection**指定每個欄位使用。 如果省略， **DisplayKey**欄位可用|  
|**DefaultMeasure**|MemberRef|模型中定義之量值的參考，或具有預設彙總函式之數值欄位的參考，以表示該量值或欄位應該做為實體的多個執行個體的預設表示。 如果省略，則使用實體執行個體的計數。|  
|**DefaultLocation**|MemberRef|欄位的參考，欄位值表示與實體執行個體相關聯的預設位置。 如果省略，則使用實體中的第一個位置欄位 (如果有)。|  
  
## <a name="field-attributes"></a>欄位屬性  
 這些屬性在 CSDL property 的子元素上定義或[NavigationProperty](http://msdn.microsoft.com/library/bb387104.aspx)項目。  
  
|屬性名稱|資料類型|Description|  
|--------------------|---------------|-----------------|  
|**ReferenceName**|Text|用於在 DAX 查詢中參考此實體的識別碼。 如果省略，則使用欄位名稱。|  
|**Caption**|Text|實體的顯示名稱。 如果省略，欄位的**ReferenceName**用。|  
|**文件集**|Text|協助商務使用者了解欄位意義的描述性文字。|  
|**Hidden**|布林|表示是否應顯示欄位。 預設值是**false**，這表示欄位會顯示。|  
|**DisplayFolder**|Text|在其中顯示此欄位的資料夾的名稱 (完整路徑)。 如果省略，則在模型根中顯示欄位。|  
|**ContextualNameRule**|Enum|值，表示是否應該根據使用內容來修改屬性名稱及其修改方式。 可能的值為：**無**，**角色**，**合併**。|  
|**對齊方式**|Enum|值，表示在表格式簡報中對齊欄位值的方式。 可能的值為**預設**， **Center**，**左**，**右邊**。 如果省略，預設會根據欄位的資料類型來決定對齊方式。|  
|**FormatString**|Text|.NET 格式字串，表示欄位值的預設格式。 如果省略，則採用下列格式：<br /><br /> 日期時間欄位： 地區的簡短日期或"d"<br /><br /> -浮點數的欄位和整數欄位，預設值彙總函式： 區域數字或"n"<br /><br /> 為沒有預設值整數彙總函式： 區域的十進位數字或"d"<br /><br /> 如果是所有其他類型的欄位，則不套用任何格式字串。|  
|**單位**|Text|套用至欄位值以表示單位的符號。 如果省略，則假設單位為未知。|  
|**寬度**|Integer|應該保留以供表格式簡報中顯示欄位值的慣用寬度 (以字元為單位)。 如果省略，預設寬度就是根據欄位的資料類型。|  
|**SortDirection**|Enum|值，表示一般的欄位值排序方式。 可能的值為**預設**，**遞增**，**遞減**。 如果省略，預設值會根據欄位的資料類型來指派排序方向。|  
|**IsRightToLeft**|布林|表示欄位是否包含應該由右至左讀取的文字。 如果省略，則採用模型設定。|  
|**OrderBy**|MemberRef|模型內另一個欄位的參考，該欄位定義此欄位之值的排序次序。 這兩個欄位的值必須具有 1:1 對應，否則排序行為是未定義的。 如果省略，欄位就會根據自己的值來排序。|  
|**目錄**|Enum|列舉，描述欄位的子類型或內容。 如果省略，則假設沒有特定的子類型，除非該欄位的資料類型為 Binary，在此情況下，則假設使用 Image。 如需支援的內容類型完整清單，請參閱 AMO 文件集。|  
|**DefaultAggregateFunction**|Enum|值，表示通常用於彙總此欄位的預設函數 (如果有)。 可能的值為**無**，**總和**，**平均**，**計數**， **Min**， **Max**. 如果省略，**總和**數值欄位，會假設**無**的所有其他欄位。|  
|**IsSimpleMeasure**|布林|表示量值是否只是數值欄位的簡單彙總。 這類彙總可以視需要在查詢中輕鬆地定義，因此應該從模型定義中省略以提高效能。 如果省略， **false**假設。|  
|**Kpi**<br /><br /> **KpiGoal**<br /><br /> **KpiStatus**|Subelement|表示量值元素要做為 KPI。 KPI 子元素使用 KpiGoal 和 KpiStauts 元素以定義相關的顯示影像和目標範圍。|  
  
  

