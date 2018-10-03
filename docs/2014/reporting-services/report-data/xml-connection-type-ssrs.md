---
title: XML 連線類型 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 5b55fff2-1b15-4156-83ef-15ad9cf9f509
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 4e47b2cc13c05438ce38d1b6f63bcbcb357c60d8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48211948"
---
# <a name="xml-connection-type-ssrs"></a>XML 連接類型 (SSRS)
  若要在報表中包含來自 XML 資料來源的資料，您必須具有以 XML 類型之報表資料來源為基礎的資料集。 此內建資料來源類型是以 XML 資料延伸模組為基礎。 請使用此資料來源類型連接至 XML 文件、Web 服務或內嵌在查詢中的 XML，並從中擷取資料。  
  
 此資料延伸模組支援與連接字串分開管理的參數和認證。  
  
 您可以使用本主題中的資訊來建置資料來源。 如需逐步指示，請參閱 <<c0> [ 加入及驗證資料連接或資料來源&#40;報表產生器及 SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)。</c0>  
  
##  <a name="Connection"></a> 連接字串  
 連接字串必須是指向 Web 服務、網路架構應用程式或可透過 HTTP 使用之 XML 文件的 URL； XML 文件的副檔名必須是 XML。 您也可以針對內嵌在資料集查詢中的 XML 資料使用空的連接字串。  
  
 下列範例分別說明 Web 服務和 XML 文件的連接字串語法。 不支援 `file://` 通訊協定。  
  
|XML 文件類型|連接字串範例|  
|-----------------------|-------------------------------|  
|Web 服務|`http://adventure-works.com/results.aspx`|  
|XML 文件|`http://localhost/XML/Customers.xml`|  
|內嵌 XML 文件|*Empty*|  
  
 如需更多連接字串範例，請參閱 [報表產生器中的資料連接、資料來源及連接字串](../data-connections-data-sources-and-connection-strings-in-report-builder.md)。  
  
##  <a name="Credentials"></a> 認證  
 需要有認證才能夠執行報表、於本機預覽報表並且從報表伺服器預覽報表。  
  
 發行報表之後，您可能需要變更資料來源的認證，如此當報表在報表伺服器上執行時，擷取資料的權限就會是有效的。  
  
 報表撰寫用戶端提供下列可用來指定認證的選項：  
  
-   目前的 Windows 使用者 (也稱為整合式安全性)。  
  
-   不需要認證。 如果您未選取認證，則會使用匿名存取。 請確定您已為報表伺服器定義自動執行帳戶，以連接到外部資料來源。 XML 資料處理延伸模組不會將認證傳遞到目標 URL 或 Web 服務。除非您已定義自動執行帳戶，否則連接不會成功。 如需詳細資訊，請參閱 msdn.microsoft.com 上《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [線上叢書](http://go.microsoft.com/fwlink/?linkid=121312)》中 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 文件的[設定自動執行帳戶 &#40;SSRS 設定管理員&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)。  
  
 不支援預存認證和提示認證。 請記住，如果您停用 Windows 整合式安全性，您就無法利用它擷取資料。 如果您指定預存認證或提示認證，執行階段中將會發生錯誤。  
  
 如需詳細資訊，請參閱 <<c0> [ 資料連接、 資料來源和 Reporting Services 中的連接字串](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)或是[在 報表產生器中指定認證](../specify-credentials-in-report-builder.md)。  
  
##  <a name="Query"></a> 查詢  
 查詢會指定要為報表資料集擷取的資料。 查詢結果集中的資料行會填入資料集的欄位集合。 報表只會處理查詢所擷取的第一個結果集。  
  
 您必須使用以文字為基礎的查詢設計工具來建立查詢； 查詢必須傳回 XML 資料。  
  
 如需以文字為基礎之查詢設計工具的詳細資訊，請參閱[以文字為基礎的查詢設計工具使用者介面 &#40;報表產生器&#41;](text-based-query-designer-user-interface-report-builder.md)。  
  
 以下為資料來源為 XML 類型時，資料集查詢的可能值。  
  
-   *空白*： 使用空的查詢來建立預設結果集。 預設查詢的建立方式，是藉由讀取資料來源，並周遊到 XML 節點階層中的第一個分葉集合。 結果集會包含所有節點，連同該路徑上的文字值和所有節點屬性； 結果集內的資料行會對應到資料集的欄位。  
  
-   元素路徑： 指定的資料來源擷取 XML 資料時要使用的節點序列。  
  
-   XML 查詢元素： 具有下列選擇性元素的 XML 查詢規格：  
  
    -   **Web 服務：**  
  
         必要的 XML 項目：  
  
         `<Method Namespace=` *"namespace"*  `Name="MethodName" />`  
  
         `-- or --`  
  
         `<SoapAction>` *soap 動作* `</SoapAction>`  
  
         選擇性 XML 元素：  
  
         `<ElementPath>`  *元素路徑*  `</ElementPath>`  
  
         `<Method Namespace=` *"namespace"*  `Name="MethodName" />`  
  
         `-- or --`  
  
         `<SoapAction>` *soap 動作* `</SoapAction>`  
  
    -   **XML 文件：**  
  
         選擇性 XML 元素：  
  
         `<ElementPath>`  *元素路徑*  `</ElementPath>`  
  
    -   **內嵌的 XML 文件：**  
  
         必要的 XML 項目：  
  
         `<XmlData>` 內部 XML `</XmlData>`  
  
         選擇性 XML 元素：  
  
         `<ElementPath>`  *元素路徑*  `</ElementPath>`  
  
         `-- or --`  
  
         `<ElementPath IgnoreNamespaces="true">`  *元素路徑*  `</ElementPath>`  
  
 如需查詢語法的詳細資訊，請參閱 msdn.microsoft.com 上《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [線上叢書](http://go.microsoft.com/fwlink/?linkid=121312)》中 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 文件的 [XML 報表資料的 XML 查詢語法 &#40;SSRS&#41;](report-data-ssrs.md)。  
  
 如需範例，請參閱 [Reporting Services：使用 XML 與 Web 服務資料來源](http://go.microsoft.com/fwlink/?LinkId=81654)。  
  
### <a name="requirements-for-retrieving-xml-web-service-data"></a>擷取 XML Web 服務資料的需求  
 XML 資料處理延伸模組不會為您偵測結構描述。 因此，您必須有某個方式可以探索哪些 SOAP 方法將擷取您想要的資料， 您也必須了解 Web 服務用於其資料的定址配置或命名空間。  
  
 如果是 Web 服務，您可以提供會指定要呼叫之方法或 SOAP 動作的 <`Query`> 元素。 如果 XML 資料來源有一個階層式結構會產生您想用於報表中的資料，可以將此查詢保留空白，並使用預設查詢。 此查詢執行時所擷取的 XML 元素節點值和屬性會對應到您用於報表中的資料集欄位。  
  
### <a name="requirements-for-retrieving-xml-document-data"></a>擷取 XML 文件資料的需求  
 使用 http 通訊協定時，伺服器必須傳回 XML 資料，或是必須將 XML 資料內嵌在 XML `Query` 元素中。 如果您使用 http 通訊協定直接參考 XML 文件，其副檔名必須是 .xml。  
  
 您必須知道如何建立 XML 查詢來擷取所有需要的資料。 如果您未指定元素路徑，剖析 XML 文件的預設行為是選取到 XML 文件中分葉節點集合的第一個可用路徑。 如果此 XML 文件包含其他同層級分葉節點集合的其他路徑，除非您在查詢中指定路徑，否則會忽略這些節點。  
  
 您可以使用類似於 XQuery 的 XML 語法提供元素路徑。  
  
 如需詳細資訊，請參閱 msdn.microsoft.com 上《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [線上叢書](http://go.microsoft.com/fwlink/?linkid=121312)》中 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 文件的 [XML 報表資料的元素路徑語法 &#40;SSRS&#41;](element-path-syntax-for-xml-report-data-ssrs.md)。  
  
##  <a name="Parameters"></a> 參數  
 系統不會分析查詢來識別參數。  
  
 若要加入參數，您必須透過 [[資料集屬性](../dataset-properties-dialog-box-parameters-report-builder.md)] 對話方塊上的 [參數] 頁面手動建立參數。  
  
##  <a name="Remarks"></a> 備註  
 XML 資料延伸模組支援從表格式而非階層式 XML 資料進行報告的功能。 如需詳細資訊，請參閱[從外部資料來源新增資料 &#40;SSRS&#41;](add-data-from-external-data-sources-ssrs.md)。  
  
 沒有提供從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫擷取 XML 文件的內建支援。  
  
##  <a name="HowTo"></a> 如何主題  
 本節包含使用資料連接、資料來源與資料集的逐步指示。  
  
 [加入及驗證資料連接或資料來源&#40;報表產生器及 SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [建立共用資料集或內嵌資料集 &#40;報表產生器及 SSRS&#41;](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [將篩選加入資料集中 &#40;報表產生器及 SSRS&#41;](add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
##  <a name="Related"></a> 相關章節  
 本文件集的這些章節會提供報表資料的深入概念性資訊，以及如何定義、自訂和使用與報表資料相關組件的程序資訊。  
  
 [將資料加入至報表&#40;報表產生器及 SSRS&#41;](report-datasets-ssrs.md)  
 提供存取報表資料的概觀。  
  
 [報表產生器中的資料連接、資料來源及連接字串](../data-connections-data-sources-and-connection-strings-in-report-builder.md)  
 提供資料連接與資料來源的相關資訊。  
  
 [報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 提供內嵌與共用資料集的相關資訊。  
  
 [資料集欄位集合 &#40;報表產生器及 SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)  
 提供查詢所產生之資料集欄位集合的相關資訊。  
  
 《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [線上叢書》](http://go.microsoft.com/fwlink/?linkid=121312)中 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 文件的 [Reporting Services 支援的資料來源 &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md)。  
 提供支援每一個資料延伸模組之平台與版本的深入資訊。  
  
## <a name="see-also"></a>另請參閱  
 [報表參數 &#40;報表產生器和報表設計師&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)   
 [篩選、分組和排序資料 &#40;報表產生器及 SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [運算式 &#40;報表產生器及 SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)  
  
  
