---
title: SAP NetWeaver BI 連線類型 (SSRS) | Microsoft Docs
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: f985856b-31d5-4e56-844b-8a8ee38da67e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 518133fc1023683f5f15af50db6133c28db2cc17
ms.sourcegitcommit: 3daacc4198918d33179f595ba7cd4ccb2a13b3c0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/25/2018
ms.locfileid: "50031563"
---
# <a name="sap-netweaver-bi-connection-type-ssrs"></a>SAP NetWeaver BI 連接類型 (SSRS)
  若要在報表中加入來自 SAP NetWeaver® Business Intelligence 外部資料來源的資料，您必須具有以 [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)]類型之報表資料來源為基礎的資料集。 這個內建的資料來源類型的建構基礎為 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework Data Provider 1.0 for [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)]的資料延伸模組。  
  
 這個資料延伸模組可以讓您從 InfoCubes、MultiProviders (虛擬 InfoCubes) 與 Web 查詢擷取多維度的資料，而這些資料來源已定義於 [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)] 外部資料來源。  
  
 您可以使用本主題中的資訊來建置資料來源。 如需逐步指示，請參閱 [加入及驗證資料連接 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)。  
  
##  <a name="Connection"></a> 連接字串  
 請洽詢資料庫管理員，以取得用來連接資料來源的連接資訊和認證。 下列連接字串範例會指定伺服器上的 [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)] 資料來源使用通訊埠 8000，並指定網際網路上的 XML for Analysis Services (XMLA) 使用 SOAP：  
  
```  
DataSource=http://mySAPNetWeaverBIServer:8000/sap/bw/xml/soap/xmla  
```  
  
 如需更多連接字串範例，請參閱 [報表產生器中的資料連接、資料來源及連接字串](https://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)。  
  
  
##  <a name="Credentials"></a> 認證  
 需要有認證才能夠執行報表、於本機預覽報表並且從報表伺服器預覽報表。  
  
 發行報表之後，您可能需要變更資料來源的認證，如此當報表在報表伺服器上執行時，擷取資料的權限就會是有效的。  
  
 如需詳細資訊，請參閱[資料連接、資料來源及連接字串 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) 或[在報表產生器中指定認證](https://msdn.microsoft.com/library/7412ce68-aece-41c0-8c37-76a0e54b6b53)。  
  
  
##  <a name="Query"></a> 查詢  
 您可以在設計模式或查詢模式中使用圖形化查詢設計工具，透過瀏覽資料來源中的基礎資料結構，建立多維度運算式 (MDX) 查詢。 在設計階段，您可以從查詢設計工具以互動方式執行查詢，來查看其結果。 您建立的查詢會定義資料集的欄位。 在執行階段，會從資料來源傳回實際的資料。 請使用圖形化查詢設計工具來執行下列動作：  
  
-   在設計模式中，將資料來源的維度、成員、成員屬性以及關鍵數值拖曳到 [資料] 窗格，以建立多維度運算式 (MDX) 查詢。 請從 [導出成員] 窗格中將導出成員拖曳到 [資料] 窗格，以定義其他資料集欄位。  
  
-   在設計模式中，將維度、成員、成員屬性以及關鍵數值拖曳到 [查詢] 窗格，或者直接在 [查詢] 窗格中輸入 MDX 文字。 請從 [導出成員] 窗格中將導出成員拖曳到 [資料] 窗格，以定義其他資料集欄位。  
  
 當您建立查詢時，查詢設計工具會自動將預設屬性加入 MDX 查詢中。 若要包含預設屬性以外的屬性，您必須手動修改 MDX 查詢。  
  
 如需使用這個查詢設計工具的詳細資訊，請參閱 [SAP NetWeaver BI 查詢設計工具使用者介面 &#40;報表產生器&#41;](https://msdn.microsoft.com/library/8edda06d-1608-498b-bd50-10905e54f6ce)。  
  
  
##  <a name="Extended"></a> 擴充欄位屬性  
 [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)] 資料來源支援擴充欄位屬性。 擴充欄位屬性是資料集欄位 **Value** 和 **IsMissing** 以外的屬性，由資料處理延伸模組所定義。 擴充屬性包括預先定義的屬性和自訂屬性。 預先定義的屬性是多個資料來源常用的屬性。 自訂屬性對於每個資料來源都是唯一的屬性。  
  
### <a name="working-with-field-properties"></a>使用欄位屬性  
 在 [報表資料] 窗格中，並不會顯示擴充欄位屬性，因為您無法將項目拖曳至報表配置上。 相反地，將該屬性的父欄位拖曳至報表，然後將預設屬性從 **Value** 變更為想要使用的屬性。 例如，如果 MDX 查詢設計工具中的 [Calendar Year/Month Level 01] 欄位名稱，是藉著從 [中繼資料] 窗格中將層級拖曳至 [查詢] 窗格所建立，則可以使用下列語法參照運算式中的 **Long Name** 自訂擴充屬性：  
  
 `=Fields!Calendar_Year_Month_Level_01("Long Name")`  
  
 當您將滑鼠指標停留在 [中繼資料] 窗格時，擴充欄位屬性的名稱會在「工具提示」中出現。 如需有關可用來瀏覽基礎資料之查詢設計工具的詳細資訊，請參閱＜ [SAP NetWeaver BI Query Designer User Interface](../../reporting-services/report-data/sap-netweaver-bi-query-designer-user-interface.md)＞。  
  
> [!NOTE]  
>  只有當報表執行以及從其資料集擷取資料時，由資料來源提供擴充欄位屬性的值，這些值才會存在。 這樣，您就可以利用以下描述的語法，從任何運算式參考那些 **Field** 屬性值。 然而，由於這些欄位是此資料提供者的特定欄位，而且不屬於報表定義語言的一部分，因此您對這些值所進行的變更並不會和報表定義儲存在一起。  
  
 請使用下列其中一個語法來參考運算式中預先定義的擴充屬性：  
  
-   *Fields!FieldName.PropertyName*  
  
-   *Fields!FieldName("PropertyName")*  
  
 請使用下列語法來參考運算式中自訂的擴充屬性：  
  
-   *Fields!FieldName("PropertyName")*  
  
  
### <a name="predefined-field-properties"></a>預先定義的欄位屬性  
 下表提供可用在 [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)] 資料來源之預先定義的欄位屬性清單。  
  
|**屬性**|**型別**|**描述或預期的值**|  
|------------------|--------------|---------------------------------------|  
|**ReplTest1**|**物件**|指定欄位的資料值。|  
|**IsMissing**|**布林**|指出在產生的資料集裡是否有找到欄位。|  
|**FormattedValue**|**String**|傳回關鍵數值的格式化值。|  
|**BackgroundColor**|**String**|傳回資料庫中為欄位定義的背景色彩。|  
|**Color**|**String**|傳回資料庫中為項目定義的前景色彩。|  
|**索引鍵**|**物件**|傳回層級的索引鍵。|  
|**LevelNumber**|**Integer**|如果是父子式階層，則會傳回層級或維度編號。|  
|**ParentUniqueName**|**String**|如果是父子式階層，會傳回父層級的完整名稱。|  
|**UniqueName**|**String**|傳回層級的完整名稱。 例如，某一位員工的 **UniqueName** 值可能是 *[0D_Company].[10D_Department].[11]*。|  
  
 如需在運算式中使用欄位及欄位屬性的詳細資訊，請參閱[運算式中的內建集合 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md)。  
  
  
##  <a name="Remarks"></a> 備註  
 這個資料提供者並沒有支援所有的報表傳遞模式。 這個資料處理延伸模組不支援透過資料驅動訂閱所傳遞的報表。 如需詳細資訊，請參閱[使用外部資料來源以取得訂閱者資料 &#40;資料驅動訂閱&#41;](../../reporting-services/subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md)。  
  
 如需詳細資訊，請參閱 [搭配 SAP NetWeaver Business Intelligence 使用 SQL Server 2008 Reporting Services](https://go.microsoft.com/fwlink/?LinkId=167352)。  
  
  
##  <a name="HowTo"></a> 如何主題  
 本節包含使用資料連接、資料來源與資料集的逐步指示。  
  
 [加入及驗證資料連接 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [建立共用資料集或內嵌資料集 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [將篩選加入資料集中 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
  
##  <a name="Related"></a> 相關章節  
 本文件集的這些章節會提供報表資料的深入概念性資訊，以及如何定義、自訂和使用與報表資料相關組件的程序資訊。  
  
 [報表資料集 &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)  
 提供存取報表資料的概觀。  
  
 [報表產生器中的資料連接、資料來源及連接字串](https://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)  
 提供資料連接與資料來源的相關資訊。  
  
 [報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 提供內嵌與共用資料集的相關資訊。  
  
 [資料集欄位集合 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
 提供查詢所產生之資料集欄位集合的相關資訊。  
  
 [Reporting Services 支援的資料來源 &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)  
 提供支援每一個資料延伸模組之平台與版本的深入資訊。  
  
  
## <a name="see-also"></a>另請參閱  
 [報表參數 &#40;報表產生器和報表設計師&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [篩選、分組和排序資料 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [運算式 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
