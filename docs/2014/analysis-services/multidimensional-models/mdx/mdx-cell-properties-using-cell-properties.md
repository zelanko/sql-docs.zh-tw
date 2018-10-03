---
title: 使用資料格屬性 (MDX) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- intrinsic cell properties [MDX]
- cells [MDX]
- cell properties [MDX]
- CELL PROPERTIES keyword
ms.assetid: a593c74d-8c5e-485e-bd92-08f9d22451d4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8aa9168e6272522bc773cb61166cb888d988c009
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48082808"
---
# <a name="using-cell-properties-mdx"></a>使用資料格屬性 (MDX)
  多維度運算式 (MDX) 的資料格屬性包含有關多維度資料來源 (如 Cube) 中資料格的內容及格式的資訊。  
  
 MDX 支援 MDX SELECT 陳述式的 CELL PROPERTIES 關鍵字，擷取內建資料格屬性。 內建資料格屬性最常用來協助資料格資料的虛擬呈現方式。  
  
## <a name="cell-properties-keyword-syntax"></a>CELL PROPERTIES 關鍵字語法  
 使用下列語法`CELL PROPERTIES`MDX 關鍵字`SELECT`陳述式：  
  
```  
SELECT [<axis_specification>  
       [, <axis_specification>...]]  
  FROM [<cube_specification>]  
[WHERE [<slicer_specification>]]  
[<cell_props>]  
```  
  
 以下語法顯示 `<cell_props>` 值的格式，以及此值如何將 `CELL PROPERTIES` 關鍵字與一或多個內建資料格屬性搭配使用：  
  
```  
<cell_props> ::= CELL PROPERTIES <property> [, <property>...]  
```  
  
## <a name="supported-intrinsic-cell-properties"></a>支援的內建資料格屬性  
 下表會將 `<property>` 值中使用的支援內建資料格屬性列出。  
  
|屬性|描述|  
|--------------|-----------------|  
|`ACTION_TYPE`|代表存在於資料格上動作類型的位元遮罩。 此屬性可以有下列其中一個值：<br /><br /> **MDACTION_TYPE_URL**<br /><br /> **MDACTION_TYPE_HTML**<br /><br /> **MDACTION_TYPE_STATEMENT**<br /><br /> **MDACTION_TYPE_DATASET**<br /><br /> **MDACTION_TYPE_ROWSET**<br /><br /> **MDACTION_TYPE_COMMANDLINE**<br /><br /> **MDACTION_TYPE_PROPRIETARY**<br /><br /> **MDACTION_TYPE_REPORT**<br /><br /> **MDACTION_TYPE_DRILLTHROUGH**<br /><br /> <br /><br /> 注意：包含 where 子句中之集合的查詢，不包括鑽研動作。|  
|**BACK_COLOR**|用以顯示 `VALUE` 或`FORMATTED_VALUE` 屬性的背景色彩。 如需詳細資訊，請參閱 [FORE_COLOR 及 BACK_COLOR 內容 &#40;MDX&#41;](mdx-cell-properties-fore-color-and-back-color-contents.md)。|  
|`CELL_ORDINAL`|資料集中資料格的序數。|  
|**FONT_FLAGS**|影響字型的位元遮罩詳細資料。 例如，值 5 代表結合了粗體 (`MDFF_BOLD`) 和底線 (`MDFF_UNDERLINE`) 字型效果。 該值是以下其中一或多個常數的位元 OR 運算結果。<br /><br /> `MDFF_BOLD` = 1<br /><br /> `MDFF_ITALIC` = 2<br /><br /> `MDFF_UNDERLINE` = 4<br /><br /> `MDFF_STRIKEOUT` = 8|  
|**FONT_NAME**|要用來顯示的字型`VALUE`或`FORMATTED_VALUE`屬性。|  
|**FONT_SIZE**|用以顯示 `VALUE` 或`FORMATTED_VALUE` 屬性的字型大小。|  
|**FORE_COLOR**|用以顯示 `VALUE` 或`FORMATTED_VALUE` 屬性的前景色彩。 如需詳細資訊，請參閱 [FORE_COLOR 及 BACK_COLOR 內容 &#40;MDX&#41;](mdx-cell-properties-fore-color-and-back-color-contents.md)。|  
|`FORMAT`|與相同`FORMAT_STRING`。|  
|`FORMAT_STRING`|用來建立的格式字串`FORMATTED_VALUE`屬性值。 如需詳細資訊，請參閱 [FORMAT_STRING 內容 &#40;MDX&#41;](mdx-cell-properties-format-string-contents.md)。|  
|`FORMATTED_VALUE`|表示格式化的顯示的字元字串`VALUE`屬性。|  
|`LANGUAGE`|將會套用 `FORMAT_STRING` 的地區設定。 `LANGUAGE` 通常用於貨幣轉換。|  
|`UPDATEABLE`|此值代表是否可更新資料格。 此屬性可以有下列其中一個值：<br /><br /> `MD_MASK_ENABLED` (0x00000000) 可以更新資料格。<br /><br /> `MD_MASK_NOT_ENABLED` (0x10000000) 無法更新資料格。<br /><br /> `CELL_UPDATE_ENABLED` (0x00000001) 可以更新資料格集中的資料格。<br /><br /> `CELL_UPDATE_ENABLED_WITH_UPDATE` (0x00000002) 可以使用 update 陳述式更新資料格。 若要更新不可寫入的分葉資料格，則該次更新可能會失敗。<br /><br /> `CELL_UPDATE_NOT_ENABLED_FORMULA` (0x10000001) 儲存格不能更新，因為資料格座標; 間的導出的成員使用一組擷取該資料格，已將它的 where 子句。 即使公式會影響資料格的值 (或是啟用導出資料格)，還是會更新資料格。 在此案例中，因為計算將會影響到結果，所以此資料格最終的值可能不是更新的值。<br /><br /> `CELL_UPDATE_NOT_ENABLED_NONSUM_MEASURE` (0x10000002) 因為無法更新非總和量值 （計數、 最小值、 最大、 相異計數、 局部加總），就無法更新資料格。<br /><br /> `CELL_UPDATE_NOT_ENABLED_NACELL_VIRTUALCUBE` (0x10000003) 因為資料格不存在於量值的交集及量值的量值群組不相關的維度成員，就無法更新資料格。<br /><br /> `CELL_UPDATE_NOT_ENABLED_SECURE` (0x10000005) 因為資料格受到保護，無法更新資料格。<br /><br /> `CELL_UPDATE_NOT_ENABLED_CALCLEVEL` (0x10000006) 保留供日後使用。<br /><br /> `CELL_UPDATE_NOT_ENABLED_CANNOTUPDATE` (0x10000007) 因為內部原因，無法更新資料格。<br /><br /> `CELL_UPDATE_NOT_ENABLED_INVALIDDIMENSIONTYPE` (0x10000009) 因為採礦模型、 間接或資料採礦維度中不支援更新，無法更新資料格。|  
|`VALUE`|未格式化的資料格值。|  
  
 只有`CELL_ORDINAL`， `FORMATTED_VALUE`，和`VALUE`資料格屬性。 `PROPERTIES` 結構描述資料列集中定義的所有內建或提供者特有的資料格屬性，包括它們的資料類型及提供者支援在內。 如需詳細資訊`PROPERTIES`結構描述資料列，請參閱 < [MDSCHEMA_PROPERTIES 資料列集](../../schema-rowsets/ole-db-olap/mdschema-properties-rowset.md)。  
  
 根據預設，如果`CELL PROPERTIES`不使用關鍵字，傳回的資料格屬性是`VALUE`， `FORMATTED_VALUE`，和`CELL_ORDINAL`（依此順序）。 如果`CELL PROPERTIES`使用關鍵字，會傳回只明確陳述關鍵字的那些資料格屬性。  
  
 下列範例示範如何使用`CELL PROPERTIES`MDX 查詢中的關鍵字：  
  
```  
SELECT  
   {[Measures].[Reseller Gross Profit]} ON COLUMNS,  
   {[Reseller].[Reseller Type].[Reseller Name].Members} ON ROWS  
FROM [Adventure Works]  
CELL PROPERTIES VALUE, FORMATTED_VALUE, FORMAT_STRING, FORE_COLOR, BACK_COLOR  
```  
  
 傳回扁平化資料列集; 的 MDX 查詢不會傳回資料格屬性如同只有在此情況下，表示每個資料格`FORMATTED_VALUE`傳回資料格屬性。  
  
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
 [MDX 查詢基礎觀念&#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)  
  
  
