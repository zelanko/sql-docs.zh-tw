---
title: "Analysis Services 資料庫的擴充欄位屬性 (SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-data
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1d7d87e2-bf0d-4ebb-a287-80b5a967a3f2
caps.latest.revision: "7"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 5d09ae6530bc9180b23a4ec81eeaeaabf1c41110
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="extended-field-properties-for-an-analysis-services-database-ssrs"></a>Analysis Services 資料庫的擴充欄位屬性 (SSRS)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料處理延伸模組支援擴充欄位屬性。 擴充欄位屬性是除了欄位屬性 **Value** 和 **IsMissing** 之外，資料來源可用而且資料處理延伸模組支援的屬性。 在 [報表資料] 窗格中，報表資料集的欄位集合中不會顯示擴充屬性。 若要在報表中包含擴充欄位屬性值，您必須撰寫運算式，使用內建 **Fields** 集合來以名稱指定擴充欄位屬性值。  
  
 擴充屬性包括預先定義的屬性和自訂屬性。 預先定義的屬性是多個資料來源共通的屬性，這類屬性會對應到特定欄位屬性名稱，而且可透過內建的 **Fields** 集合按照名稱存取。 自訂屬性則是各個資料提供者專有的屬性，這類屬性可透過內建的 **Fields** 集合存取，但只能透過使用擴充屬性名稱作為字串的語法。  
  
 當您使用圖形模式的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] MDX 查詢設計工具定義查詢時，預先定義的資料格屬性和維度屬性集合就會自動加入至 MDX 查詢中。 您只可以使用明確列在您報表的 MDX 查詢中的擴充屬性。 依報表的不同，您或許想修改預設的 MDX 命令文字，藉此包括 Cube 中定義的其他維度或自訂屬性。 如需 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料來源中可用之擴充欄位的詳細資訊，請參閱[建立和使用屬性值 &#40;MDX&#41;](http://msdn.microsoft.com/library/0cafb269-03c8-4183-b6e9-220f071e4ef2)。  
  
## <a name="working-with-field-properties-in-a-report"></a>使用報表中的欄位屬性  
 擴充欄位屬性包含預先定義的屬性和資料提供者特有的屬性。 即使欄位屬性位於針對資料集所建立的查詢中，還是不會與欄位清單一起出現在 **[報表資料]** 窗格內，因此您無法將欄位屬性拖曳到報表設計介面上。 不過，您必須將欄位拖曳到報表上，然後將該欄位的 **Value** 屬性變更為您要使用的屬性。 例如，如果 Cube 中的資料格資料已經格式化，您可以利用以下運算式來使用 FormattedValue 欄位屬性： `=Fields!FieldName.FormattedValue`。  
  
 若要參考未預先定義的擴充屬性，請在運算式中使用下列語法：  
  
-   *Fields!FieldName("PropertyName")*  
  
## <a name="predefined-field-properties"></a>預先定義的欄位屬性  
 在大多數情況下，預先定義的欄位屬性會套用至量值、層級或維度。 預先定義的欄位屬性必須有儲存在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料來源中的對應值。 如果值不存在，或者 (例如) 您在層級上指定了僅限量值的欄位屬性，則屬性會傳回 Null 值。  
  
 您可以使用下列任一語法，從運算式參考預先定義的屬性：  
  
-   *Fields!FieldName.PropertyName*  
  
-   *Fields!FieldName("PropertyName")*  
  
 下表提供您可以使用之預先定義的欄位屬性清單。  
  
|**屬性**|**型別**|**描述或預期的值**|  
|------------------|--------------|---------------------------------------|  
|**Value**|**物件**|指定欄位的資料值。|  
|**IsMissing**|**布林**|指出在產生的資料集裡是否有找到欄位。|  
|**UniqueName**|**字串**|傳回層級的完整名稱。 例如，某一位員工的 **UniqueName** 值可能是 *[Employee].[Employee Department].[Department].&[Sales].&[North American Sales Manager].&[272]*。|  
|**BackgroundColor**|**字串**|傳回資料庫中為欄位定義的背景色彩。|  
|**Color**|**字串**|傳回資料庫中為項目定義的前景色彩。|  
|**FontFamily**|**字串**|傳回資料庫中為項目定義之字型的名稱。|  
|**FontSize**|**字串**|傳回資料庫中為項目定義之字型的點數大小。|  
|**FontWeight**|**字串**|傳回資料庫中為項目定義之字型的粗細。|  
|**FontStyle**|**字串**|傳回資料庫中為項目定義之字型的樣式。|  
|**TextDecoration**|**字串**|傳回資料庫中為項目定義的特殊文字格式。|  
|**FormattedValue**|**字串**|傳回量值或關鍵數值的格式化值。 例如， **[銷售量配額]** 的 **FormattedValue** 屬性會傳回貨幣格式，如 $1,124,400.00。|  
|**索引鍵**|**物件**|傳回層級的索引鍵。|  
|**LevelNumber**|**Integer**|如果是父子式階層，則會傳回層級或維度編號。|  
|**ParentUniqueName**|**字串**|如果是父子式階層，會傳回父層級的完整名稱。|  
  
> [!NOTE]  
>  當報表為其資料集執行及擷取資料時，只有在資料來源 (例如 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Cube) 提供這些值的情況下，這些擴充欄位屬性的值才會存在。 這樣，您就可以利用以下章節所述的語法，從任何運算式參考那些欄位屬性值。 不過，由於這些欄位是此資料提供者的特定欄位，因此，您對這些值所作的變更不會隨同報表定義一併儲存。  
  
### <a name="example-extended-properties"></a>擴充屬性範例  
 為了示範說明擴充屬性，下列 MDX 查詢和結果集之中包含從為 Cube 定義的維度屬性中取得的數個成員屬性。 這些成員屬性包括 MEMBER_CAPTION、UNIQUENAME、Properties("Day Name")、MEMBER_VALUE、PARENT_UNIQUE_NAME 和 MEMBER_KEY。  
  
 這個 MDX 查詢會針對 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 範例資料庫中所包含之 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] DW 資料庫內的 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] Cube 來執行。  
  
```  
WITH MEMBER [Measures].[DateCaption]   
      AS '[Date].[Date].CURRENTMEMBER.MEMBER_CAPTION'   
   MEMBER [Measures].[DateUniqueName]   
      AS '[Date].[Date].CURRENTMEMBER.UNIQUENAME'   
   MEMBER [Measures].[DateDayName]   
      AS '[Date].[Date].Properties("Day Name")'   
   MEMBER [Measures].[DateValueinOriginalDatatype]   
      AS '[Date].[Date].CURRENTMEMBER.MEMBER_VALUE'   
   MEMBER [Measures].[DateParentUniqueName]   
      AS '[Date].[Date].CURRENTMEMBER.PARENT_UNIQUE_NAME'   
   MEMBER [Measures].[DateMemberKeyinOriginalDatatype]   
      AS '[Date].[Date].CURRENTMEMBER.MEMBER_KEY'   
SELECT {  
   [Measures].[DateCaption],   
   [Measures].[DateUniqueName],   
   [Measures].[DateDayName],   
   [Measures].[DateValueinOriginalDatatype],  
   [Measures].[DateParentUniqueName],  
   [Measures].[DateMemberKeyinOriginalDatatype]  
   } ON COLUMNS , [Date].[Date].ALLMEMBERS ON ROWS   
FROM [Adventure Works]  
  
```  
  
 在 MDX 查詢窗格中執行這個查詢時，結果集會包含 1158 個資料列， 前四個資料列如下表所示。  
  
|DateCaption|DateUniqueName|DateDayName|DateValueinOriginalDatatype|DateParentUniqueName|DateMemberKeyinOriginalDatatype|  
|-----------------|--------------------|-----------------|---------------------------------|--------------------------|-------------------------------------|  
|All Periods|[Date].[Date].[All Periods]|(Null)|(Null)|(Null)|0|  
|1-Jul-01|[Date].[Date].&[1]|星期日|7/1/2001|[Date].[Date].[All Periods]|1|  
|2-Jul-01|[Date].[Date].&[2]|星期一|7/2/2001|[Date].[Date].[All Periods]|2|  
|3-Jul-01|[Date].[Date].&[3]|星期二|7/3/2001|[Date].[Date].[All Periods]|3|  
  
 在圖形模式 MDX 查詢設計工具中所建置的預設 MDX 查詢只包含維度屬性的 MEMBER_CAPTION 和 UNIQUENAME。 依預設，這些值一定是 **String**資料類型。  
  
 如果成員屬性必須保持原始資料類型，您可以在以文字為基礎的查詢設計工具中修改預設的 MDX 陳述式，以包含另一個屬性 MEMBER_VALUE。 在下列簡單的 MDX 陳述式中，已在要擷取的維度屬性清單中加入 MEMBER_VALUE。  
  
```  
SELECT NON EMPTY {[Measures].[Order Count]} ON COLUMNS,   
NON EMPTY { ([Date].[Month of Year].[Month of Year] ) }   
DIMENSION PROPERTIES   
   MEMBER_CAPTION, MEMBER_UNIQUE_NAME, MEMBER_VALUE ON ROWS   
FROM [Adventure Works]  
CELL PROPERTIES   
   VALUE, BACK_COLOR, FORE_COLOR,   
   FORMATTED_VALUE, FORMAT_STRING,   
   FONT_NAME, FONT_SIZE, FONT_FLAGS  
```  
  
 MDX 結果窗格中前四個結果資料列顯示於下表中。  
  
|Month of Year|Order Count|  
|-------------------|-----------------|  
|一月|2,481|  
|二月|2,684|  
|三月|2,749|  
|四月|2,739|  
  
 這些屬性雖然是 MDX 選取陳述式的一部分，但是卻不會出現在結果集資料行中， 然而，報表還是可以透過使用擴充屬性功能來使用這些資料。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]的 MDX 查詢結果窗格中，按兩下資料格即可查看資料格屬性值 (如果 Cube 中已設定的話)。 如果按兩下包含 1,379 的第一個 [Order Count] 資料格，就會出現內含下列資料格屬性的快顯視窗：  
  
|屬性|Value|  
|--------------|-----------|  
|CellOrdinal|0|  
|Value|2481|  
|BACK_COLOR|(Null)|  
|FORE_COLOR|(Null)|  
|FORMATTED_VALUE|2,481|  
|FORMAT_STRING|#,#|  
|FONT_NAME|(Null)|  
|FONT_SIZE|(Null)|  
|FONT_FLAGS|(Null)|  
  
 如果用這個查詢建立報表資料集，並將資料集繫結至資料表，就可以看到欄位的預設 VALUE 屬性，例如 `=Fields!Month_of_Year!Value`。 如果將這個運算式設定為資料表的排序運算式，結果資料表將會依月份的字母順序排序，因為 Value 欄位會使用 **String** 資料類型。 若要將資料表的排序順序設為依月份在當年出現的順序，一月最前，十二月最後，則請使用下列運算式：  
  
```  
=Fields!Month_of_Year("MEMBER_VALUE")  
```  
  
 這會將欄位值依其在資料來源中的原始整數資料類型排序。  
  
## <a name="see-also"></a>另請參閱  
 [運算式 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [運算式中的內建集合 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md)   
 [資料集欄位集合 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
  
  
