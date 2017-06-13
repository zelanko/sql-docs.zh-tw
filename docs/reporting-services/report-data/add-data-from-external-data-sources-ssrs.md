---
title: "將資料加入從外部資料來源 (SSRS) |Microsoft 文件"
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
ms.assetid: 924a2ec3-150c-4bb2-83c9-4c7b440e8c03
caps.latest.revision: 12
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 76e09d1f90d7eb2f3d91aef60e4ce2a9c671ab13
ms.contentlocale: zh-tw
ms.lasthandoff: 06/13/2017

---
# <a name="add-data-from-external-data-sources-ssrs"></a>從外部資料來源加入資料 (SSRS)
  若要從外部資料來源擷取資料，可以使用資料連接。 資料連接資訊通常是由外部資料來源的擁有者提供，此擁有者負責授與權限和指定要使用的認證類型。 資料連接資訊會儲存為報表資料來源。 資料來源類型會指定要用來擷取資料的資料延伸模組。  
  
 如需資料來源類型的詳細資訊，請參閱 [本節內容](#InThisSection)。  
  
##  <a name="DataAccess"></a> 了解資料存取技術  
 為了擷取報表的資料，資料集會需要多層資料存取軟體。 下列清單提供簡單的描述，說明報表使用資料存取技術的方式。  
  
-   **應用程式和使用者介面** ：報表產生器應用程式，用來建立資料來源、加入共用資料來源的參考、加入共用資料集，或是加入包含所依據之資料來源和資料集的報表組件。  
  
-   **報表定義元素** ：資料來源和資料集是報表定義的組件。 將報表發行至報表伺服器之後，就可以將共用資料來源和共用資料集與報表分開管理。  
  
    -   **資料來源和共用資料來源** ：報表定義的組件，其中包括有關資料處理延伸模組的類型、連接資訊以及驗證。  
  
    -   **資料集和欄位集合** ：報表定義的組件，其中包括查詢、欄位集合和欄位資料類型。  
  
-   **Reporting Services 資料延伸模組** ：內建的資料延伸模組，會隨報表產生器一併安裝。 資料延伸模組提供可處理驗證、伺服器彙總和多值參數的功能。  
  
-   **資料提供者** ：管理外部資料來源連接和資料擷取的軟體。 資料提供者會定義連接字串語法。 大部分資料延伸模組都是在資料提供者層之上建立。  
  
-   **外部資料來源** ：擷取報表資料的來源，例如資料庫、檔案、Cube 或 Web 服務。  
  
> [!NOTE]  
>  當您未連接至報表伺服器時，可以選擇隨報表產生器一併安裝的資料延伸模組。 您可以使用電腦上的認證，以單一使用者身分存取資料。 當您連接至報表伺服器時，可以選擇安裝在報表伺服器上的資料延伸模組。 您會以執行報表的其中一位使用者身分存取資料，而且您會使用報表伺服器上的認證。 如需詳細資訊，請參閱 [在報表產生器中指定認證](http://msdn.microsoft.com/library/7412ce68-aece-41c0-8c37-76a0e54b6b53)。  
  
##  <a name="ReportData"></a> 了解報表資料  
 報表會以最簡單的形式在報表頁面的資料區中，顯示報表資料集的資料，也就是使用單一資料表、圖表、矩陣或其他類型的報表資料區。 報表資料集的資料來自從單一查詢命令傳回的第一個結果集，該命令是以外部資料來源的唯讀存取權執行。 每一個資料區都會視需要展開，以顯示資料集中的所有資料。  
  
 資料集的資料基本上是表格式。 資料行是資料集查詢中的欄位。 資料列則來自結果集中的資料列。 您可以在報表中使用下列通用類型的資料：  
  
-   矩形資料。 來自結果集的資料，其中每一個資料列擁有相同數目的資料行。  
  
-   階層式資料可支援做為扁平化資料列集。  
  
    -   不支援不完全階層 (其中每一個資料列的資料擁有不同的資料行數目)。 對某些資料延伸模組而言，這種情況具有某些隱含意義。  
  
    -   搭配多維資料來源使用的資料延伸模組會使用 XML 做為分析通訊協定，並且會將資料當做扁平化資料列集，而不是當做資料格集擷取。  
  
    -   XML 資料延伸模組會自動扁平化 XML 資料，以便在報表中使用。 如果 XML 元素的第一個執行個體未包含所有屬性或子元素，則資料可能無法做為報表資料使用。  
  
-   支援遞迴的資料。 包含遞迴資料階層的結果集，會包括矩形結果集中階層結構的所有相關資訊。 例如，公司內的主管-下屬 (Report-to) 結構可以透過包括兩個資料行的資料表呈現：員工與經理。 每位經理也是另一位經理的員工。 最上層的經理通常包含 null 或某些其他識別碼，表示此員工沒有經理。  
  
  
##  <a name="DataTypes"></a> 使用資料類型  
 當您建立資料集時，欄位的資料類型會從 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]對應到 Common Language Runtime (CLR) 資料類型的子集。 無法明確對應的資料類型會以字串的形式傳回。 如需使用欄位資料類型的詳細資訊，請參閱 [資料集欄位集合 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)。 當您建立參數時，資料類型必須是支援的報表定義資料類型。 如需將資料類型從資料提供者對應到報表參數的詳細資訊，請參閱[運算式中的資料類型 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)。  
  
  
##  <a name="HowTo"></a> 如何主題  
 本節包含使用資料連接、資料來源與資料集的逐步指示。  
  
 [加入及驗證資料連接 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [建立共用資料集或內嵌資料集 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [將篩選加入資料集中 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
  
##  <a name="InThisSection"></a> 本節內容  
 下列主題提供有關每一個內建資料延伸模組的資訊。  
  
|主題|資料來源類型|  
|-----------|----------------------|  
|[SQL Server 連接類型 &#40;SSRS&#41;](../../reporting-services/report-data/sql-server-connection-type-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|[MDX 的 Analysis Services 連接類型 &#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-mdx-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|  
|[Power Pivot 連接類型 &#40;SSRS&#41;](../../reporting-services/report-data/power-pivot-connection-type-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|  
|[SharePoint 清單連接類型 &#40;SSRS&#41;](../../reporting-services/report-data/sharepoint-list-connection-type-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] SharePoint 清單|  
|[SQL Azure 連接類型 &#40;SSRS&#41;](../../reporting-services/report-data/sql-azure-connection-type-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDS](../../includes/sssds-md.md)]|  
|[SQL Server Parallel Data Warehouse 連接類型 &#40;SSRS&#41;](../../reporting-services/report-data/sql-server-parallel-data-warehouse-connection-type-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDWfull](../../includes/ssdwfull-md.md)]|  
|[SAP NetWeaver BI 連接類型 &#40;SSRS&#41;](../../reporting-services/report-data/sap-netweaver-bi-connection-type-ssrs.md)|SAP NetWeaver BI|  
|[Hyperion Essbase 連接類型 &#40;SSRS&#41;](../../reporting-services/report-data/hyperion-essbase-connection-type-ssrs.md)|Hyperion Essbase|  
|[OLE DB 連接類型 &#40;SSRS&#41;](../../reporting-services/report-data/ole-db-connection-type-ssrs.md)|OLE DB|  
|[ODBC 連接類型 &#40;SSRS&#41;](../../reporting-services/report-data/odbc-connection-type-ssrs.md)|ODBC|  
|[XML 連接類型 &#40;SSRS&#41;](../../reporting-services/report-data/xml-connection-type-ssrs.md)|XML|  
|[報表模型連接 &#40;SSRS&#41;](../../reporting-services/report-data/report-model-connection-ssrs.md)|.smdl 模型|  
  
  
##  <a name="Related"></a> 相關章節  
 本文件集的這些章節會提供報表資料的深入概念性資訊，以及如何定義、自訂和使用與報表資料相關組件的程序資訊。  
  
|主題|說明|  
|-----------|-----------------|  
|[報表資料集 &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)|提供存取報表資料的概觀。|  
|[報表產生器中的資料連接、資料來源及連接字串](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)|提供資料連接與資料來源的相關資訊。|  
|[報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)|提供內嵌與共用資料集的相關資訊。|  
|[資料集欄位集合 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)|提供查詢所產生之資料集欄位集合的相關資訊。|  
|《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [線上叢書》](http://go.microsoft.com/fwlink/?linkid=121312)中 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 文件的 [Reporting Services 支援的資料來源 &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)。|提供支援每一個資料延伸模組之平台與版本的深入資訊。|  
|《[](../../reporting-services/extensions/data-processing/data-processing-extensions-overview.md) 線上叢書 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 》中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [Books Online](http://go.microsoft.com/fwlink/?linkid=121312).|為進階使用者提供資料延伸模組的深入資訊。|  
  
  
## <a name="see-also"></a>請參閱＜  
 [報表資料集 &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [查詢設計工具 &#40;報表產生器&#41;](http://msdn.microsoft.com/library/553f0d4e-8b1d-4148-9321-8b41a1e8e1b9)  
  
  
