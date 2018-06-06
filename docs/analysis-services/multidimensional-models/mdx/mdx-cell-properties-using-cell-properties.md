---
title: 使用資料格屬性 (MDX) |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 481d89abac98dee1095e55a9890cea100f6c4db6
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="mdx-cell-properties---using-cell-properties"></a>MDX 資料格屬性的使用資料格屬性
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  多維度運算式 (MDX) 的資料格屬性包含有關多維度資料來源 (如 Cube) 中資料格的內容及格式的資訊。  
  
 MDX 支援 MDX SELECT 陳述式的 CELL PROPERTIES 關鍵字，擷取內建資料格屬性。 內建資料格屬性最常用來協助資料格資料的虛擬呈現方式。  
  
## <a name="cell-properties-keyword-syntax"></a>CELL PROPERTIES 關鍵字語法  
 對 MDX **SELECT** 陳述式的 **CELL PROPERTIES** 關鍵字使用以下語法：  
  
```  
SELECT [<axis_specification>  
       [, <axis_specification>...]]  
  FROM [<cube_specification>]  
[WHERE [<slicer_specification>]]  
[<cell_props>]  
```  
  
 以下語法顯示 `<cell_props>` 值的格式，以及此值如何將 **CELL PROPERTIES** 關鍵字與一或多個內建資料格屬性搭配使用：  
  
```  
<cell_props> ::= CELL PROPERTIES <property> [, <property>...]  
```  
  
## <a name="supported-intrinsic-cell-properties"></a>支援的內建資料格屬性  
 下表會將 `<property>` 值中使用的支援內建資料格屬性列出。  
  
|屬性|Description|  
|--------------|-----------------|  
|**ACTION_TYPE**|代表存在於資料格上動作類型的位元遮罩。 此屬性可以有下列其中一個值：<br /><br /> **MDACTION_TYPE_URL**<br /><br /> **MDACTION_TYPE_HTML**<br /><br /> **MDACTION_TYPE_STATEMENT**<br /><br /> **MDACTION_TYPE_DATASET**<br /><br /> **MDACTION_TYPE_ROWSET**<br /><br /> **MDACTION_TYPE_COMMANDLINE**<br /><br /> **MDACTION_TYPE_PROPRIETARY**<br /><br /> **MDACTION_TYPE_REPORT**<br /><br /> **MDACTION_TYPE_DRILLTHROUGH**<br /><br /> <br /><br /> 注意：包含 where 子句中之集合的查詢，不包括鑽研動作。|  
|**BACK_COLOR**|用以顯示 **VALUE** 或 **FORMATTED_VALUE** 屬性的背景色彩。 如需詳細資訊，請參閱 [FORE_COLOR 及 BACK_COLOR 內容 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-properties-fore-color-and-back-color-contents.md)。|  
|**CELL_ORDINAL**|資料集中資料格的序數。|  
|**FONT_FLAGS**|影響字型的位元遮罩詳細資料。 該值是以下其中一或多個常數的位元 OR 運算結果。<br /><br /> **MDFF_BOLD** = 1<br /><br /> **MDFF_ITALIC** = 2<br /><br /> **MDFF_UNDERLINE** = 4<br /><br /> **MDFF_STRIKEOUT** = 8<br /><br /> <br /><br /> 例如，值 5 表示結合了粗體 (**MDFF_BOLD**) 及底線 (**MDFF_UNDERLINE**) 字型效果。|  
|**FONT_NAME**|顯示 **VALUE** 或 **FORMATTED_VALUE** 屬性所使用的字型。|  
|**FONT_SIZE**|顯示 **VALUE** 或 **FORMATTED_VALUE** 屬性所使用的字型大小。|  
|**FORE_COLOR**|用以顯示 **VALUE** 或 **FORMATTED_VALUE** 屬性的前景色彩。 如需詳細資訊，請參閱 [FORE_COLOR 及 BACK_COLOR 內容 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-properties-fore-color-and-back-color-contents.md)。|  
|**FORMAT**|與 **FORMAT_STRING**相同。|  
|**FORMAT_STRING**|用以建立 **FORMATTED_VALUE** 屬性值的格式字串。 如需詳細資訊，請參閱 [FORMAT_STRING 內容 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-properties-format-string-contents.md)。|  
|**FORMATTED_VALUE**|代表格式化顯示 **VALUE** 屬性的字元字串。|  
|**LANGUAGE**|將會套用 **FORMAT_STRING** 的地區設定。 **LANGUAGE** 通常用於貨幣轉換。|  
|**UPDATEABLE**|此值代表是否可更新資料格。 此屬性可以有下列其中一個值：|  
||**MD_MASK_ENABLED** (0x00000000)   可以更新資料格。|  
||**MD_MASK_NOT_ENABLED** (0x10000000)   無法更新資料格。|  
||**CELL_UPDATE_ENABLED** (0x00000001)   可以更新資料格集的資料格。|  
||**CELL_UPDATE_ENABLED_WITH_UPDATE** (0x00000002)   可以更新陳述式更新資料格。 若要更新不可寫入的分葉資料格，則該次更新可能會失敗。|  
||**CELL_UPDATE_NOT_ENABLED_FORMULA** (0x10000001)   因為資料格的座標間有導出成員，所以無法更新資料格；是以 where 子句中的集合擷取該資料格。 即使公式會影響資料格的值 (或是啟用導出資料格)，還是會更新資料格。 在此案例中，因為計算將會影響到結果，所以此資料格最終的值可能不是更新的值。|  
||**CELL_UPDATE_NOT_ENABLED_NONSUM_MEASURE** (0x10000002)   因為無法更新非總和量值 (計數、最小、最大、相異計數、局部加總)，所以無法更新資料格。|  
||**CELL_UPDATE_NOT_ENABLED_NACELL_VIRTUALCUBE** (0x10000003)   因為資料格不存在於量值及與量值的量值群組不相關之維度成員的交集，所以無法更新資料格。|  
||**CELL_UPDATE_NOT_ENABLED_SECURE** (0x10000005)    因為資料格受到保護，所以無法更新。|  
||**CELL_UPDATE_NOT_ENABLED_CALCLEVEL** (0x10000006)   保留供日後使用。|  
||**CELL_UPDATE_NOT_ENABLED_CANNOTUPDATE** (0x10000007)   因為內部原因，所以無法更新資料格。|  
||**CELL_UPDATE_NOT_ENABLED_INVALIDDIMENSIONTYPE** (0x10000009)   因為採礦模型、間接或資料採礦維度中不支援更新，所以無法更新資料格。|  
|**VALUE**|未格式化的資料格值。|  
  
 只需要 **CELL_ORDINAL**、 **FORMATTED_VALUE**和 **VALUE** 資料格屬性。 **PROPERTIES** 結構描述資料列集中定義的所有內建或提供者特有的資料格屬性，包括它們的資料類型及提供者支援。 如需 **PROPERTIES** 結構描述資料列集的詳細資訊，請參閱 [MDSCHEMA_PROPERTIES 資料列集](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-properties-rowset.md)。  
  
 依預設，如未使用 **CELL PROPERTIES** 關鍵字，傳回的資料格屬性會是 **VALUE**、 **FORMATTED_VALUE**和 **CELL_ORDINAL** (依此順序)。 如果使用 **CELL PROPERTIES** 關鍵字，只會傳回明確陳述關鍵字的那些資料格屬性。  
  
 以下範例說明 MDX 查詢中 **CELL PROPERTIES** 關鍵字的用法：  
  
```  
SELECT  
   {[Measures].[Reseller Gross Profit]} ON COLUMNS,  
   {[Reseller].[Reseller Type].[Reseller Name].Members} ON ROWS  
FROM [Adventure Works]  
CELL PROPERTIES VALUE, FORMATTED_VALUE, FORMAT_STRING, FORE_COLOR, BACK_COLOR  
```  
  
 傳回扁平化資料列集的 MDX 查詢不會傳回資料格屬性；在此狀況下，會如同只有傳回 **FORMATTED_VALUE** 資料格屬性一般，呈現每個資料格 。  
  
## <a name="setting-cell-properties"></a>設定資料格屬性  
 資料格屬性可以在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 的各種不同位置設定。 例如，[格式字串] 屬性可以針對 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]中 Cube 編輯器之 [Cube 結構] 索引標籤上的一般量值進行設定；此外還可以針對 Cube 編輯器的 [計算] 索引標籤上 Cube 所定義的導出量值進行設定；查詢之 WITH 子句中定義的導出量值也會在此定義其格式字串。下列查詢將示範如何在導出量值上設定資料格屬性：  
  
```  
WITH MEMBER MEASURES.CELLPROPERTYDEMO AS [Measures].[Internet Sales Amount]  
, FORE_COLOR=RGB(0,0,255)  
, BACK_COLOR=IIF([Measures].[Internet Sales Amount]>7000000, RGB(255,0,0), RGB(0,255,0))  
, FONT_SIZE=10  
, FORMAT_STRING='#,#.000'  
SELECT MEASURES.CELLPROPERTYDEMO ON 0,  
[Date].[Calendar Year].[Calendar Year].MEMBERS ON 1  
FROM [Adventure Works]  
CELL PROPERTIES VALUE, FORMATTED_VALUE, FORE_COLOR, BACK_COLOR, FONT_SIZE  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 查詢基礎觀念 & #40;Analysis Services & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  
