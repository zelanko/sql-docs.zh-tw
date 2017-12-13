---
title: "內建成員屬性 (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: intrinsic member properties [MDX]
ms.assetid: 84e6fe64-9b37-4e79-bedf-ae02e80bfce8
caps.latest.revision: "41"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: cf5daff8843fab7cdf1aed4acd0fec0dec84e5ea
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="mdx-member-properties---intrinsic-member-properties"></a>MDX 成員屬性內建成員屬性
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)][!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]公開內建屬性，您可以在自訂應用程式中，會傳回額外的資料或中繼資料使用，或協助模型調查或建構的查詢中包含的維度成員上。 如果您使用 SQL Server 用戶端工具，您可以在 SQL Server Management Studio (SSMS) 中檢視內建屬性。  
  
 內建屬性包括 **ID**、 **KEY**、 **KEYx**和 **NAME**，這些屬性可在任何層級公開給每位成員。 您也可以傳回位置資訊，例如 **LEVEL_NUMBER** 或 **PARENT_UNIQUE_NAME**，以及其他資訊。  
  
 取決於您如何建立查詢以及用來執行查詢的用戶端應用程式，成員屬性不一定會顯示在結果集中。 如果您使用 SQL Server Management Studio 測試或執行查詢，您可以按兩下結果集中的成員，即可開啟 [成員屬性] 對話方塊，顯示每個內建成員屬性的值。  
  
 如需有關使用及檢視維度成員屬性的簡介，請參閱 [在 SSMS 的 MDX 查詢視窗中檢視 SSAS 成員屬性](http://go.microsoft.com/fwlink/?LinkId=317362)。  
  
> [!NOTE]  
>  因為提供者符合 OLE DB 規格的 OLAP 小節 (1999 年 3 月 (2.6 節))，所以 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 支援此主題中列出的內建成員屬性。  
>   
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 以外的提供者可支援其他內建成員屬性。 如需其他提供者支援之內建成員屬性的詳細資訊，請參閱這些提供者提供的文件。  
  
## <a name="types-of-member-properties"></a>成員屬性類型  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 支援的內建成員屬性有兩種類型：  
  
 區分內容的成員屬性  
 這些成員屬性必須用於特定階層或層級的內容，而且要將值提供給指定維度或層級的每個成員。  
  
 請注意下列範例如何加入 **KEY** 屬性的路徑： `MEMBER [Measures].[Parent Member Key] AS [Product].[Product Categories].CurrentMember.Parent.PROPERTIES("KEY")`。  
  
 不區分內容的成員屬性  
 這些成員屬性無法用於特定維度或層級的內容，並且會傳回座標軸上所有成員的值。  
  
 不易受內容影響的屬性是獨立的，而且不包含路徑資訊。 請注意，在下列範例中，沒有為 **PARENT_UNIQUE_NAME** 指定維度或層級： `DIMENSION PROPERTIES PARENT_UNIQUE_NAME ON COLUMNS`  
  
 不管內建成員屬性是否會區分內容，都適用以下使用方式規則：  
  
-   您只能指定座標軸上預計之維度成員相關的內建成員屬性。  
  
-   您可以利用不區分內容的內建成員屬性，在同一個查詢中混合區分內容的成員屬性要求。  
  
-   您可以使用 **PROPERTIES** 關鍵字以查詢屬性。  
  
 以下各節將描述 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中可用的各種區分內容及不區分內容的內建成員屬性，以及如何將 **PROPERTIES** 關鍵字與每種屬性類型搭配使用。  
  
## <a name="context-sensitive-member-properties"></a>區分內容的成員屬性  
 所有維度成員及層級成員支援區分內容的內建成員屬性清單。 下表列出這些區分內容的屬性。  
  
|屬性|說明|  
|--------------|-----------------|  
|**ID**|內部維護用的成員識別碼。|  
|**Key**|原始資料類型的成員索引鍵值。 MEMBER_KEY 是為回溯相容性而提供。  對於非複合索引鍵，MEMBER_KEY 的值與 KEY0 相同，對於複合索引鍵，MEMBER_KEY 屬性為 Null。|  
|**KEYx**|成員的索引鍵，其中 x 是索引鍵以零為基底的序數。 KEY0 可用於複合和非複合索引鍵，但主要是用於複合索引鍵。<br /><br /> 關於複合索引鍵，KEY0、KEY1、KEY2 等等，共同形成複合索引鍵。 您可以在查詢中單獨使用每一項，藉以傳回複合索引鍵的該部分。 例如，指定 KEY0 可傳回複合索引鍵的第一個部分，指定 KEY1 傳回複合索引鍵的下一部分，依此類推。<br /><br /> 如果索引鍵為非複合鍵，則 KEY0 相當於 **Key**。<br /><br /> 請注意， **KEYx** 可用於內容中，也可以在沒有內容的情況下使用。 因此，兩個清單上都有它。<br /><br /> 如需如何使用此成員屬性的範例，請參閱 [簡單的 MDX 小知識：Key0、Key1、Key2](http://go.microsoft.com/fwlink/?LinkId=317364)。|  
|**Name**|成員的名稱。|  
  
### <a name="properties-syntax-for-context-sensitive-properties"></a>區分內容屬性的 PROPERTIES 語法  
 您可以在特定維度或層級的內容中使用這些成員屬性，而且要將值提供給指定維度或階層的每個成員。  
  
 對於維度成員屬性，您可以在屬性名稱前面加上套用該屬性的維度名稱。 下列範例會顯示適當語法：  
  
 `DIMENSION PROPERTIES Dimension.Property_name`  
  
 對於層級成員屬性，您可以在屬性名稱前面，只加上層級名稱，或者對於其他規格，則可加上維度及層級名稱。 下列範例會顯示適當語法：  
  
 `DIMENSION PROPERTIES [Dimension.]Level.Property_name`  
  
 為了方便說明，您要傳回 `[Sales]` 維度中每個參考成員的所有名稱。 若要傳回這些名稱，您要在多維度運算式 (MDX) 查詢中使用以下陳述式：  
  
 `DIMENSION PROPERTIES [Sales].Name`  
  
## <a name="non-context-sensitive-member-properties"></a>不區分內容的成員屬性  
 所有成員支援同樣不顧內容的內建成員屬性清單。 這些屬性能提供應用程式可用以加強使用者經驗的其他資訊。  
  
 下表列出 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]支援的不區分內容內建屬性。  
  
> [!NOTE]  
>  MEMBERS 結構描述資料列集中的資料行支援下表列出的內建成員屬性。 如需 **MEMBERS** 結構描述資料列集的詳細資訊，請參閱 [MDSCHEMA_MEMBERS 資料列集](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-members-rowset.md)。  
  
|屬性|說明|  
|--------------|-----------------|  
|**CATALOG_NAME**|此一成員所屬 Cube 的名稱。|  
|**CHILDREN_CARDINALITY**|成員擁有的子系數目。 這可為一個估計值，因此您不應該依賴此值做為確實計數。 提供者應會傳回最佳的可能估計值。|  
|**CUSTOM_ROLLUP**|自訂成員運算式。|  
|**CUSTOM_ROLLUP_PROPERTIES**|自訂成員屬性。|  
|**DESCRIPTION**|成員的可讀取描述。|  
|**DIMENSION_UNIQUE_NAME**|此一成員所屬維度的唯一名稱。 對於會依識別資格產生唯一名稱的提供者，此名稱的每個元件會使用分隔符號。|  
|**HIERARCHY_UNIQUE_NAME**|階層架構的唯一名稱。 如果該成員屬於多個階層，該成員所屬的每個階層都會有一個資料列。 對於會依識別資格產生唯一名稱的提供者，此名稱的每個元件會使用分隔符號。|  
|**IS_DATAMEMBER**|指出成員是否為資料成員的布林值。|  
|**IS_PLACEHOLDERMEMBER**|表示成員是否為預留位置的布林值。|  
|**KEYx**|成員的索引鍵，其中 x 是索引鍵以零為基底的序數。 KEY0 可用於複合和非複合索引鍵。<br /><br /> 如果索引鍵為非複合鍵，則 KEY0 相當於 **Key**。<br /><br /> 關於複合索引鍵，KEY0、KEY1、KEY2 等等，共同形成複合索引鍵。 您可以在查詢中單獨參考每一項，藉以傳回複合索引鍵的該部分。 例如，指定 KEY0 可傳回複合索引鍵的第一個部分，指定 KEY1 傳回複合索引鍵的下一部分，依此類推。<br /><br /> 請注意， **KEYx** 可用於內容中，也可以在沒有內容的情況下使用。 因此，兩個清單上都有它。<br /><br /> 如需如何使用此成員屬性的範例，請參閱 [簡單的 MDX 小知識：Key0、Key1、Key2](http://go.microsoft.com/fwlink/?LinkId=317364)。|  
|**LCID** *x*|以地區設定識別碼十六進位值翻譯的成員標題，其中 *x* 是地區設定識別碼十進位值 (例如，代表加拿大英文的 LCID1009)。 只有當翻譯的標題資料行繫結至資料來源時，才適用此功能。|  
|**LEVEL_NUMBER**|成員距根階層的距離。 根層級為零。|  
|**LEVEL_UNIQUE_NAME**|成員所屬層級的唯一名稱。 對於會依識別資格產生唯一名稱的提供者，此名稱的每個元件會使用分隔符號。|  
|**MEMBER_CAPTION**|與該成員關聯的標籤或標題。 標題主要是供顯示之用。 如果標題不存在，查詢就會傳回 **MEMBER_NAME**。|  
|**MEMBER_KEY**|原始資料類型的成員索引鍵值。 MEMBER_KEY 是為回溯相容性而提供。  對於非複合索引鍵，MEMBER_KEY 的值與 KEY0 相同，對於複合索引鍵，MEMBER_KEY 屬性為 Null。|  
|**MEMBER_NAME**|成員的名稱。|  
|**MEMBER_TYPE**|成員的類型。 此屬性可以有下列其中一個值：<br /><br /> **MDMEMBER_TYPE_REGULAR**<br /><br /> **MDMEMBER_TYPE_ALL**<br /><br /> **MDMEMBER_TYPE_FORMULA**<br /><br /> **MDMEMBER_TYPE_MEASURE**<br /><br /> **MDMEMBER_TYPE_UNKNOWN**<br /><br /> <br /><br /> 注意：MDMEMBER_TYPE_FORMULA 優先於 MDMEMBER_TYPE_MEASURE。 因此，如果 Measures 維度有一個公式 (導出) 成員，導出成員的 **MEMBER_TYPE** 屬性為 MDMEMBER_TYPE_FORMULA。|  
|**MEMBER_UNIQUE_NAME**|成員的唯一名稱。 對於會依識別資格產生唯一名稱的提供者，此名稱的每個元件會使用分隔符號。|  
|**MEMBER_VALUE**|原始類型的成員值。|  
|**PARENT_COUNT**|此成員擁有的父系數目。|  
|**PARENT_LEVEL**|成員的父系距階層之根層級的距離。 根層級為零。|  
|**PARENT_UNIQUE_NAME**|成員之父系的唯一名稱。 如果是根層級的任何成員，則會傳回**NULL** 。 對於會依識別資格產生唯一名稱的提供者，此名稱的每個元件會使用分隔符號。|  
|**SKIPPED_LEVELS**|略過的成員層級數目。|  
|**UNARY_OPERATOR**|成員的一元運算子。|  
|**UNIQUE_NAME**|成員的完整名稱以此格式表示：[維度]、[層級]、[key6]。|  
  
### <a name="properties-syntax-for-non-context-sensitive-properties"></a>不區分內容屬性的 PROPERTIES 語法  
 使用以下語法指定會使用 **PROPERTIES** 關鍵字的內建、不區分內容的成員屬性：  
  
 `DIMENSION PROPERTIES Property`  
  
 請注意，此語法不允許依維度或層級限定屬性。 因為座標軸的所有成員套用了不區分內容的內建成員屬性，所以無法限定屬性。  
  
 例如，指定 **DESCRIPTION** 內建成員屬性的 MDX 陳述式會有以下語法：  
  
 `DIMENSION PROPERTIES DESCRIPTION`  
  
 此陳述式會傳回座標軸維度中每個成員的描述。 若要以 *Dimension*`.DESCRIPTION` 或 *Level*`.DESCRIPTION`的維度或層級嘗試限定屬性，則無法驗證該陳述式。  
  
### <a name="example"></a>範例  
 下列範例顯示傳回內建屬性的 MDX 查詢。  
  
 **範例 1：在查詢中使用會受內容影響的內建屬性**  
  
 下列範例會傳回父系識別碼、索引鍵和每項產品類別的名稱。 請注意屬性如何公開為量值。 在您執行查詢時，這可讓您在資料格集中檢視屬性，而非 SSMS 的 [成員屬性] 對話方塊。 您可以執行類似此項目的查詢，以便從已部署的 Cube 擷取成員中繼資料。  
  
```  
WITH  
MEMBER [Measures].[Parent Member ID] AS  
 [Product].[Product Categories].CurrentMember.Parent.PROPERTIES("ID")  
MEMBER [Measures].[Parent Member Key] AS  
 [Product].[Product Categories].CurrentMember.Parent.PROPERTIES("KEY")  
MEMBER [Measures].[Parent Member Name] AS  
 [Product].[Product Categories].CurrentMember.Parent.PROPERTIES("Name")  
SELECT  
 {[Measures].[Parent Member ID], [Measures].[Parent Member Key], [Measures].[Parent Member Name] } on COLUMNS,   
 [Product].[Product Categories].AllMembers on ROWS  
FROM [Adventure Works]  
```  
  
 **範例 2：不受內容影響的內建屬性**  
  
 下列範例是不受內容影響的內建屬性完整清單。 在 SSMS 執行查詢後，請按一下個別成員，檢視 [成員屬性] 對話方塊中的屬性。  
  
```  
SELECT [Measures].[Sales Amount Quota] on COLUMNS,  
[Employee].[Employees].members  
DIMENSION PROPERTIES  
 CATALOG_NAME ,   
 CHILDREN_CARDINALITY ,  
 CUSTOM_ROLLUP ,   
 CUSTOM_ROLLUP_PROPERTIES ,   
 DESCRIPTION ,   
 DIMENSION_UNIQUE_NAME ,   
 HIERARCHY_UNIQUE_NAME ,  
 IS_DATAMEMBER ,   
 IS_PLACEHOLDERMEMBER ,   
 KEY0 ,  
 LCID ,  
 LEVEL_NUMBER ,  
 LEVEL_UNIQUE_NAME ,  
 MEMBER_CAPTION ,   
 MEMBER_KEY ,   
 MEMBER_NAME ,   
 MEMBER_TYPE ,  
 MEMBER_UNIQUE_NAME ,   
 MEMBER_VALUE ,   
 PARENT_COUNT ,   
 PARENT_LEVEL ,   
 PARENT_UNIQUE_NAME ,  
 SKIPPED_LEVELS ,   
 UNARY_OPERATOR ,   
 UNIQUE_NAME    
 ON ROWS  
FROM [Adventure Works]  
WHERE [Employee].[Employee Department].[Department].&[Sales]  
```  
  
 **範例 3：傳回做為結果集資料的成員屬性**  
  
 下列範例會針對指定的地區設定，傳回 Adventure Works Cube 中 Product 維度的產品類別目錄成員的已翻譯標題。  
  
```  
WITH   
MEMBER Measures.CategoryCaption AS Product.Category.CurrentMember.MEMBER_CAPTION  
MEMBER Measures.SpanishCategoryCaption AS Product.Category.CurrentMember.Properties("LCID3082")  
MEMBER Measures.FrenchCategoryCaption AS Product.Category.CurrentMember.Properties("LCID1036")  
SELECT   
{ Measures.CategoryCaption, Measures.SpanishCategoryCaption, Measures.FrenchCategoryCaption } ON 0  
,[Product].[Category].MEMBERS ON 1  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>請參閱  
 [PeriodsToDate &#40;MDX&#41;](../../../mdx/periodstodate-mdx.md)   
 [子系 &#40;MDX &#41;](../../../mdx/children-mdx.md)   
 [Hierarchize &#40;MDX &#41;](../../../mdx/hierarchize-mdx.md)   
 [Count &#40;集合&#41; &#40;MDX&#41;](../../../mdx/count-set-mdx.md)   
 [篩選 &#40;MDX &#41;](../../../mdx/filter-mdx.md)   
 [AddCalculatedMembers &#40;MDX &#41;](../../../mdx/addcalculatedmembers-mdx.md)   
 [DrilldownLevel &#40;MDX &#41;](../../../mdx/drilldownlevel-mdx.md)   
 [屬性 &#40;MDX &#41;](../../../mdx/properties-mdx.md)   
 [PrevMember &#40;MDX &#41;](../../../mdx/prevmember-mdx.md)   
 [使用成員屬性 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-member-properties.md)   
 [MDX 函數參考 &#40;MDX &#41;](../../../mdx/mdx-function-reference-mdx.md)  
  
  
