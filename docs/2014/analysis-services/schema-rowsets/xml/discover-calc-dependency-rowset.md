---
title: DISCOVER_CALC_DEPENDENCY 資料列集 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- DISCOVER_CALC_DEPENDENCIES rowset
ms.assetid: f39dde72-fa5c-4c82-8b4e-88358aa2e422
caps.latest.revision: 19
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 57f839d6c50208828de3441ec6e3c5f5f77c67c6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37297238"
---
# <a name="discovercalcdependency-rowset"></a>DISCOVER_CALC_DEPENDENCY 資料列集
  報告計算之間的相依性和這些計算中所參考的物件。 您可以在用戶端應用程式中使用此資訊，針對複雜公式的問題進行報告，或在相關物件遭到刪除或修改時發出警告。 您還可以使用資料列集來擷取量值或導出資料行中使用的 DAX 運算式。  
  
 **適用於：** 表格式模型  
  
## <a name="rowset-columns"></a>資料列集資料行  
 `DISCOVER_CALC_DEPENDENCY`資料列集包含下列資料行。 資料表也會指定資料類型、指示資料行是否可以限制傳回的資料列，並提供每一個資料行的描述。  
  
|資料行名稱|類型指標|限制|描述|  
|-----------------|--------------------|-----------------|-----------------|  
|`DATABASE_NAME`|`DBTYPE_WSTR`|是|指定包含要求其相依性分析之物件的資料庫名稱。 如果省略，就會使用目前的資料庫。<br /><br /> `DISCOVER_DEPENDENCY_CALC`使用此資料行也可以限制資料列集。|  
|`OBJECT_TYPE`|`DBTYPE_WSTR`|是|表示要求其相依性分析之物件的類型。 物件必須是下列其中一種類型：<br /><br /> -   `ACTIVE_RELATIONSHIP`： 作用中的關聯性<br />-   `CALC_COLUMN`： 導出資料行<br />-   `HIERARCHY`： 階層<br />-   `MEASURE`： 量值<br />-   `RELATIONSHIP`： 關聯性<br />-   `KPI`: KPI （關鍵效能指標）<br /><br /> `DISCOVER_DEPENDENCY_CALC`使用此資料行也可以限制資料列集。|  
|`QUERY`|`DBTYPE_WSTR`|是|如果是在 [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] 中建立的表格式模型，您可以包含 DAX 查詢或運算式，以顯示該查詢或運算式的相依性圖表。 QUERY 限制會提供用戶端應用程式一個方式來判斷 DAX 查詢使用哪些物件。<br /><br /> `QUERY` 限制可以在 XMLA 或 DMV 查詢的 WHERE 子句中指定。 如需詳細資訊，請參閱＜範例＞一節。|  
|`TABLE`|`DBTYPE_WSTR`||包含產生其相依性資訊之物件的資料表名稱。|  
|`OBJECT`|`DBTYPE_WSTR`||產生其相依性資訊之物件的名稱。 如果物件是量值或導出資料行，請使用量值的名稱。 如果物件是關聯性，則是包含參與關聯性之資料行的資料表 (或 Cube 維度) 名稱。|  
|`EXPRESSION`|`DBTYPE_WSTR`||包含尋找其相依性之物件的公式。|  
|`REFERENCED_OBJECT_TYPE`|`DBTYPE_WSTR`||傳回與所參考物件具有相依性之物件的類型。 傳回的物件可以是下列其中一種類型：<br /><br /> -   `CALC_COLUMN`： 導出資料行<br />-   `COLUMN`： 資料行<br />-   `MEASURE`： 量值<br />-   `RELATIONSHIP`： 關聯性<br />-   `KPI`: KPI （關鍵效能指標）|  
|`REFERENCED_TABLE`|`DBTYPE_ WSTR`||包含相依物件之資料表的名稱。|  
|`REFERENCED_OBJECT`|`DBTYPE_ WSTR`||與所參考物件具有相依性之物件的名稱。 若是量值和導出資料行，則為量值或資料行的名稱。 若是關聯性，則是包含相依物件之資料表 (或 Cube 維度) 的完整名稱。|  
|`REFERENCED_EXPRESSION`|`DBTYPE_WSTR`||與所參考物件相依之導出資料行或量值中的公式。|  
  
## <a name="example"></a>範例  
 **基本語法**  
  
 下列查詢是簡單的 DMV 查詢，它使用目前連接的預設資料庫，傳回此資料列集中所有資料行的值。 您可以在 MDX 查詢視窗中執行此查詢並在 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] 中檢視其結果。 您也可以依照 [從 Excel 查詢 PowerPivot DMV](http://go.microsoft.com/fwlink/?LinkID=235146) 中所述的技巧，在 Excel 中檢視 DMV 查詢結果。  
  
```  
SELECT * FROM $System.DISCOVER_CALC_DEPENDENCY  
```  
  
## <a name="example"></a>範例  
 **排序結果**  
  
 加入 ORDER BY，依照資料表或另一個資料行排序資料列集。  
  
```  
SELECT * FROM $System.DISCOVER_CALC_DEPENDENCY ORDER BY [TABLE] ASC  
```  
  
## <a name="example"></a>範例  
 **使用 WHERE 子句篩選**  
  
 下一個查詢示範如何使用 WHERE 子句加入限制。 下列資料行可以當做 WHERE 子句中的查詢篩選器： `Database_Name`， `Object_Type`，和`Query`。  
  
```  
SELECT * From $SYSTEM.DISCOVER_CALC_DEPENDENCY WHERE OBJECT_TYPE = 'RELATIONSHIP' OR OBJECT_TYPE = 'ACTIVE_RELATIONSHIP'  
```  
  
## <a name="example"></a>範例  
 **篩選量值和導出資料行，以檢視基礎 DAX 運算式**  
  
 在此查詢中，你可以選取量值或導出資料行，然後檢視計算中使用的 DAX 運算式。 EXPRESSION 資料行包含 DAX 運算式。 如果您使用 DISCOVER_CALC_DEPENDENCY 來擷取模型中使用的 DAX 運算式，此查詢足以用於此用途。 它會以遞增順序傳回模型中使用的所有運算式。  
  
```  
SELECT * From $SYSTEM.DISCOVER_CALC_DEPENDENCY WHERE OBJECT_TYPE = 'MEASURE' OR OBJECT_TYPE = 'CALC_COLUMN' ORDER BY [EXPRESSION] ASC  
```  
  
## <a name="example"></a>範例  
 **使用 QUERY 篩選**  
  
 您可以使用 QUERY 限制來提供 DAX 查詢，以檢視該查詢中使用的所有物件。 假設有一個類似 ‘Evaluate Customer’ 的簡單查詢。 如同範例中所示，這個查詢會傳回客戶資料的資料列，其中資料列撰寫是根據 Customer 資料表中的資料行。 如果您現在使用 ‘Evaluate Customer’ 的 QUERY 限制來執行 DISCOVER_CALC_DEPENDENCY，您會得到該查詢中使用的資料行 (或物件)。 在這個案例中，它是 Customer 資料表中的資料行清單。  
  
 下一個查詢集合示範 QUERY 限制的語法。 您可以針對 [AdventureWorks 表格式模型 SQL Server 2012](http://msftdbprodsamples.codeplex.com/releases/view/55330) 執行這些查詢，以檢視結果集。  
  
 第一個查詢會針對包含空格的物件名稱示範如何指定 QUERY 限制。 取自 [經由 OLE DB 和 ADOMD.NET 執行 DAX 查詢](http://go.microsoft.com/fwlink/?LinkId=254329)的第二個查詢是比較複雜的查詢，其中包含多個資料表的物件。  
  
> [!NOTE]  
>  雖然查詢似乎使用雙引號，但實際上只使用單引號。 一對單引號括住 ' Evaluate\<資料表名稱 >'，而且需要成對使用加以逸出單引號括住資料表名稱使用。 只有包含空格的資料表名稱才需要資料表名稱周圍的單引號。  
  
```  
SELECT * From $SYSTEM.DISCOVER_CALC_DEPENDENCY WHERE QUERY = 'EVALUATE ''Reseller Sales'''  
```  
  
```  
SELECT * from $system.DISCOVER_CALC_DEPENDENCY WHERE QUERY = 'EVALUATE CALCULATETABLE(VALUES(''Product Subcategory''[Product Subcategory Name]), ''Product Category''[Product Category Name] = "Bikes")'  
```  
  
## <a name="example"></a>範例  
 **QUERY 限制 XMLA 範例**  
  
 您可以使用 XMLA Discover 命令傳回資料表中的查詢物件。 XMLA 會傳回原始 XML 形式的結果。 您可以使用 ADOMD.NET，以更容易讀取的格式來剖析結果。  
  
```  
<Discover xmlns="urn:schemas-microsoft-com:xml-analysis">  
   <RequestType>DISCOVER_CALC_DEPENDENCY</RequestType>  
     <Restrictions>  
        <RestrictionList>  
            <QUERY>Evaluate 'Reseller Sales'</QUERY>  
        </RestrictionList>  
    </Restrictions>  
    <Properties />  
</Discover>  
```  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 傳回資料列集  
 使用 ADOMD.NET 和結構描述資料列集來擷取中繼資料時，您可以使用 GUID 或字串，在 GetSchemaDataSet 方法中參考結構描述資料列集物件。 如需詳細資訊，請參閱 [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md)。  
  
 下表將提供可識別此資料列集的 GUID 和字串值。  
  
|引數|值|  
|--------------|-----------|  
|GUID|a07ccd46-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|DependencyGraph|  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 結構描述資料列集](../analysis-services-schema-rowsets.md)   
 [使用動態管理檢視&#40;Dmv&#41;若要監視 Analysis Services](../../instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)  
  
  
