---
title: "Hyperion Essbase 連線類型 (SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 108a00b6-799f-4066-b796-da59e95c09fd
caps.latest.revision: "10"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: b04a9b00e87526b4ea030ff6359d0969e84f11cb
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="hyperion-essbase-connection-type-ssrs"></a>Hyperion Essbase 連接類型 (SSRS)
  若要在報表中包含來自 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] 外部資料來源的資料，您必須具有以 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)]類型之報表資料來源為基礎的資料集。 這種內建資料來源類型的建構基礎是 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)]的資料延伸模組，而這個延伸模組可以讓您從 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] 外部資料來源擷取多維度資料。  
  
 您可以使用本主題中的資訊來建置資料來源。 如需逐步指示，請參閱 [加入及驗證資料連接 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)。  
  
##  <a name="Connection"></a> 連接字串  
 下列連接字串範例會指定伺服器上的 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] 資料來源使用通訊埠 13080，並指定網際網路上的 XML for [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] (XMLA) 使用 SOAP，以連接到範例目錄：  
  
```  
Data Source=http://localhost:13080/aps/XMLA; Initial Catalog=Sample  
```  
  
 如需連接字串範例的詳細資訊，請參閱 [報表產生器中的資料連接、資料來源及連接字串](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)。  
  
  
##  <a name="Credentials"></a> 認證  
 需要有認證才能夠執行報表、於本機預覽報表並且從報表伺服器預覽報表。  
  
 發行報表之後，您可能需要變更資料來源的認證，如此當報表在報表伺服器上執行時，擷取資料的權限就會是有效的。  
  
 如需詳細資訊，請參閱[資料連接、資料來源及連接字串 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) 或[在報表產生器中指定認證](http://msdn.microsoft.com/library/7412ce68-aece-41c0-8c37-76a0e54b6b53)。  
  
  
##  <a name="Query"></a> 查詢  
 您可以利用下列方式指定查詢：  
  
-   以互動方式建立查詢。 請於設計模式或查詢模式中使用圖形化查詢設計工具，在外部資料來源中瀏覽中繼資料，並以多維度運算式 (MDX) 語法產生查詢。  
  
    -   **設計檢視** ：將維度、成員、成員屬性、量值和 KPI 從中繼資料瀏覽器拖曳到 **[資料]** 窗格，以建立 MDX 查詢。 請將導出成員從 [導出成員] 窗格拖曳到 [資料] 窗格，以便建立其他資料集欄位。  
  
    -   **查詢檢視** ：將維度、成員、成員屬性、量值和 KPI 從中繼資料瀏覽器拖曳到 [查詢] 窗格，以建立 MDX 查詢。 您可以在 [查詢] 窗格中直接編輯 MDX 文字。 請將導出成員從 [導出成員] 窗格拖曳到 [查詢] 窗格，以便定義其他資料集欄位。  
  
     如需詳細資訊，請參閱 [Hyperion Essbase 查詢設計工具使用者介面 &#40;報表產生器&#41;](http://msdn.microsoft.com/library/d89a6773-dbe5-48e5-bda9-db0e67100696)。  
  
-   從報表匯入現有的 MDX 查詢。 請使用 **[匯入查詢]** 按鈕來瀏覽到 .rdl 檔案，然後匯入查詢。 您可以從包含以 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] 資料來源為基礎之內嵌資料集的報表匯入查詢。 不支援直接從 .mdx 檔案匯入 MDX 查詢。  
  
 在執行階段中，執行查詢以檢視結果集。 在您建立查詢之後，請在 [報表資料] 窗格中檢視從中繼資料產生的資料集欄位集合。 當報表執行時，實際資枓會從外部資料來源傳回。  
  
 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] 資料處理延伸模組支援擴充資料集欄位屬性。 這些值可從外部資料來源取得，但是不會出現在 [報表資料] 窗格中。 如需詳細資訊，請參閱本主題後面的＜ [擴充欄位屬性](#Extended) ＞。  
  
  
##  <a name="Parameters"></a> 若要包含查詢參數，請在查詢設計工具的篩選區域中建立篩選，然後再將該篩選標示成參數。 系統會針對每一個篩選自動建立一個資料集，以提供可用的值。 根據預設，這些資料集不會出現在 [報表資料] 窗格內。 如需詳細資訊，請參閱[針對多維度資料的參數值顯示隱藏的資料集 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-data/show-hidden-datasets-for-parameter-values-multidimensional-data.md)。  
  
 根據預設，每個報表參數都具有 **[文字]**資料類型。 建立報表參數後，您可能必須變更預設值。 如需詳細資訊，請參閱 [報表參數 &#40;報表產生器和報表設計師&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)類型之報表資料來源為基礎的資料集。  
  
  
##  <a name="Extended"></a> 擴充欄位屬性  
 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] 資料處理延伸模組支援擴充欄位屬性。 擴充欄位屬性是資料集欄位 **Value** 和 **IsMissing** 以外的屬性，由資料處理延伸模組所定義。 擴充屬性包括預先定義的屬性和自訂屬性。 預先定義的屬性是多個資料來源常用的屬性。 自訂屬性對於每個資料來源都是唯一的屬性。  
  
 在 [報表資料] 窗格中，並不會顯示擴充欄位屬性，因為您無法將項目拖曳至報表配置上。 相反地，將該屬性的父欄位拖曳至報表，然後將預設屬性從 **Value** 變更為想要使用的屬性。  
  
 當您在查詢設計工具中，將滑鼠指標停留在 [中繼資料] 窗格中的欄位時，工具提示中會出現擴充欄位屬性的名稱。 如需有關可用來瀏覽基礎資料之查詢設計工具的詳細資訊，請參閱＜ [Hyperion Essbase Query Designer User Interface](../../reporting-services/report-data/hyperion-essbase-query-designer-user-interface.md)＞。  
  
> [!NOTE]  
>  只有在 MDX 運算式中包含擴充欄位屬性值，而且資料來源會在您的報表執行並擷取其資料集之資料時提供這些值，擴充欄位屬性的值才會存在。 這樣，您就可以利用以下章節所述的語法，從任何運算式參考那些 **Field** 屬性值。 然而，由於這些欄位是此資料提供者的特定欄位，而且不屬於報表定義語言的一部分，因此您對這些值所進行的變更並不會和報表定義儲存在一起。  
  
  
### <a name="predefined-field-properties"></a>預先定義的欄位屬性  
 預先定義的欄位屬性一般是由多個資料提供者支援，而且會出現在報表資料集的 MDX 基礎查詢中。 例如，MDX 維度屬性 MEMBER_UNIQUE_NAME 會對應到預先定義的報表資料集欄位屬性 **UniqueName**。 若要在文字方塊中包含唯一的名稱值，請使用運算式 `=Fields!`\<欄位名稱>`.UniqueName`。  
  
 下表提供可用在 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] 資料來源之預先定義的欄位屬性清單。  
  
|**屬性**|**型別**|**描述或預期的值**|  
|------------------|--------------|---------------------------------------|  
|**Value**|**物件**|指定欄位的資料值。<br /><br /> 若是維度屬性，這會對應到 MEMBER_CAPTION。 若是量值，則會對應到資料值。|  
|**IsMissing**|**布林**|指出在產生的資料集裡是否有找到欄位。|  
|**FormattedValue**|**字串**|傳回關鍵數值的格式化值。<br /><br /> 從 MDX 運算式中的 FORMATTED_VALUE 對應。|  
|**BackgroundColor**|**字串**|傳回資料庫中為欄位定義的背景色彩。<br /><br /> 從 MDX 運算式中的 BACK_COLOR 對應。|  
|**Color**|**字串**|傳回資料庫中為項目定義的前景色彩。<br /><br /> 從 MDX 運算式中的 FORE_COLOR 對應。|  
|**UniqueName**|**字串**|傳回層級的完整名稱。<br /><br /> 從 MDX 運算式中的 MEMBER_UNIQUE_NAME 對應。|  
  
 如需如何在運算式中使用欄位及欄位屬性的詳細資訊，請參閱 [Built-in Collections in Expressions &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md) (運算式中的內建集合 (報表產生器及 SSRS))。  
  
  
### <a name="custom-properties"></a>自訂屬性  
 自訂欄位屬性是由資料提供者支援，而且會出現在報表資料集的 MDX 基礎查詢中，但不會出現在報表的 [資料集] 窗格中，當做該資料集下的欄位。 例如， **[Long Names]** 是一個針對維度層級而定義的成員屬性。 若要在文字方塊中包含值，您可以使用運算式 `=Fields!`\<欄位名稱>`("Long Names")`。 運算式中的欄位名稱會區分大小寫。  
  
 請使用下列語法來參考運算式中自訂的擴充屬性：  
  
-   *Fields!FieldName("PropertyName")*  
  
 下表顯示可用於 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] 資料來源的自訂欄位屬性。  
  
|**屬性**|**型別**|**描述或預期的值**|  
|------------------|--------------|---------------------------------------|  
|**FORMAT_STRING**|**字串**|在量值上的定義，這是可當做 String 類型使用的 **FormattedValue** 。|  
  
  
##  <a name="Remarks"></a> 備註  
 這個資料提供者並沒有支援所有的報表傳遞模式。 這個資料處理延伸模組不支援透過資料驅動訂閱所傳遞的報表。 如需詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [線上叢書](http://go.microsoft.com/fwlink/?linkid=121312)》中 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 文件的[使用外部資料來源以取得訂閱者資料 &#40;資料驅動訂閱&#41;](../../reporting-services/subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md)。  
  
 如需詳細資訊，請參閱＜ [使用 SQL Server 2005 Reporting Services 搭配 Hyperion Essbase](http://go.microsoft.com/fwlink/?LinkId=81970)＞。  
  
  
##  <a name="HowTo"></a> 如何主題  
 本節包含使用資料連接、資料來源與資料集的逐步指示：  
  
 [加入及驗證資料連接 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [建立共用資料集或內嵌資料集 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [將篩選加入資料集中 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
  
##  <a name="Related"></a> 相關章節  
 本文件集的這些章節會提供報表資料的深入概念性資訊，以及如何定義、自訂和使用與報表資料相關組件的程序資訊。  
  
 [報表資料集 &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)  
 提供存取報表資料的概觀。  
  
 [報表產生器中的資料連接、資料來源及連接字串](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)  
 提供資料連接與資料來源的相關資訊。  
  
 [報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 提供內嵌與共用資料集的相關資訊。  
  
 [資料集欄位集合 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
 提供資料集查詢所產生之欄位集合的相關資訊。  
  
 《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [線上叢書》](http://go.microsoft.com/fwlink/?linkid=121312)中 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 文件的 [Reporting Services 支援的資料來源 &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)。  
 提供支援每一個資料延伸模組之平台與版本的深入資訊。  
  
 [使用 SQL Server 2005 Reporting Services 搭配 Hyperion Essbase](http://go.microsoft.com/fwlink/?LinkId=81970)  
 提供有關使用這個資料延伸模組的詳細資訊。  
  
  
## <a name="see-also"></a>另請參閱  
 [報表參數 &#40;報表產生器和報表設計師&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [篩選、分組和排序資料 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [運算式 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
