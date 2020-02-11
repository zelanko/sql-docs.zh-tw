---
title: 從外部資料來源加入資料 (SSRS)
ms.prod: sql-server-2014
ms.technology: reporting-services
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 04/27/2017
ms.openlocfilehash: 54358529577061ad99c634fa6cc4ce9d98792e0c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67412686"
---
# <a name="add-data-from-external-data-sources-ssrs"></a>從外部資料來源加入資料 (SSRS)

若要從外部資料來源擷取資料，可以使用資料連接。 資料連接資訊通常是由外部資料來源的擁有者提供，此擁有者負責授與權限和指定要使用的認證類型。 資料連接資訊會儲存為報表資料來源。 資料來源類型會指定要用來擷取資料的資料延伸模組。  

##  <a name="DataAccess"></a>瞭解資料存取技術  

為了擷取報表的資料，資料集會需要多層資料存取軟體。 下列清單提供簡單的描述，說明報表使用資料存取技術的方式。  

-   **應用程式和使用者介面**您用來建立資料來源的報表產生器應用程式、加入共用資料來源的參考、加入共用資料集，或加入包含所相依之資料來源和資料集的報表元件。  

-   **報表定義元素**資料來源和資料集是報表定義的一部分。 將報表發行至報表伺服器之後，就可以將共用資料來源和共用資料集與報表分開管理。  

  -   **資料來源和共用資料來源**報表定義的一部分，其中包含有關資料處理延伸模組、連接資訊和驗證類型的資訊。  

  -   **資料集和欄位集合**包含查詢、欄位集合和欄位資料類型之報表定義的一部分。  

-   **Reporting Services 資料延伸**模組隨報表產生器安裝的內建資料延伸模組。 資料延伸模組提供可處理驗證、伺服器彙總和多值參數的功能。  

-   **資料提供者**此軟體會管理來自外部資料源之資料的連接和抓取。 資料提供者會定義連接字串語法。 大部分資料延伸模組都是在資料提供者層之上建立。  

-   **外部資料源**從何處取得報表資料，例如資料庫、檔案、cube 或 Web 服務。  

> [!NOTE]  
>  當您未連接至報表伺服器時，可以選擇隨報表產生器一併安裝的資料延伸模組。 您可以使用電腦上的認證，以單一使用者身分存取資料。 當您連接至報表伺服器時，可以選擇安裝在報表伺服器上的資料延伸模組。 您會以執行報表的其中一位使用者身分存取資料，而且您會使用報表伺服器上的認證。 如需詳細資訊，請參閱 [在報表產生器中指定認證](../specify-credentials-in-report-builder.md)。  

##  <a name="ReportData"></a>瞭解報表資料  
報表會以最簡單的形式在報表頁面的資料區中，顯示報表資料集的資料，也就是使用單一資料表、圖表、矩陣或其他類型的報表資料區。 報表資料集的資料來自從單一查詢命令傳回的第一個結果集，該命令是以外部資料來源的唯讀存取權執行。 每一個資料區都會視需要展開，以顯示資料集中的所有資料。  

資料集的資料基本上是表格式。 資料行是資料集查詢中的欄位。 資料列則來自結果集中的資料列。 您可以在報表中使用下列通用類型的資料：  

-   矩形資料。 來自結果集的資料，其中每一個資料列擁有相同數目的資料行。  

-   階層式資料可支援做為扁平化資料列集。  

  -   不支援不完全階層 (其中每一個資料列的資料擁有不同的資料行數目)。 對某些資料延伸模組而言，這種情況具有某些隱含意義。  

  -   搭配多維資料來源使用的資料延伸模組會使用 XML 做為分析通訊協定，並且會將資料當做扁平化資料列集，而不是當做資料格集擷取。  

  -   XML 資料延伸模組會自動扁平化 XML 資料，以便在報表中使用。 如果 XML 元素的第一個執行個體未包含所有屬性或子元素，則資料可能無法做為報表資料使用。  

-   支援遞迴的資料。 包含遞迴資料階層的結果集，會包括矩形結果集中階層結構的所有相關資訊。 例如，公司內的主管-下屬 (Report-to) 結構可以透過包括兩個資料行的資料表呈現：員工與經理。 每位經理也是另一位經理的員工。 最上層的經理通常包含 null 或某些其他識別碼，表示此員工沒有經理。  



##  <a name="DataTypes"></a>使用資料類型  
當您建立資料集時，欄位的資料類型會從 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]對應到 Common Language Runtime (CLR) 資料類型的子集。 無法明確對應的資料類型會以字串的形式傳回。 如需使用欄位資料類型的詳細資訊，請參閱 [資料集欄位集合 &#40;報表產生器及 SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)。 當您建立參數時，資料類型必須是支援的報表定義資料類型。 如需將資料類型從資料提供者對應到報表參數的詳細資訊，請參閱[運算式中的資料類型 &#40;報表產生器及 SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)。  



##  <a name="HowTo"></a> 如何主題  
本節包含使用資料連接、資料來源與資料集的逐步指示。  

[加入及驗證資料連線或資料來源 &#40;報表產生器和 SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)  

[建立共用資料集或內嵌資料集 &#40;報表產生器和 SSRS&#41;](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  

[將篩選加入至資料集 &#40;報表產生器和 SSRS&#41;](add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  

## <a name="InThisSection"></a> 本節內容  

下列主題提供有關每一個內建資料延伸模組的資訊。  

|主題|資料來源類型|  
|-----------|----------------------|  
|[SQL Server &#40;SSRS&#41;的連線類型](sql-server-connection-type-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|[適用于 MDX &#40;SSRS 的 Analysis Services 連線類型&#41;](analysis-services-connection-type-for-mdx-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|  
|[&#40;SSRS&#41;的 PowerPivot 連線類型](power-pivot-connection-type-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|  
|[SharePoint 清單連線類型 &#40;SSRS&#41;](sharepoint-list-connection-type-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)]SharePoint 清單|  
|[&#40;SSRS&#41;的 SQL Azure 連線類型](sql-azure-connection-type-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDS](../../includes/sssds-md.md)]|  
|[SQL Server 的平行資料倉儲連線類型 &#40;SSRS&#41;](sql-server-parallel-data-warehouse-connection-type-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDWfull](../../includes/ssdwfull-md.md)]|  
|[&#40;SSRS&#41;的 SAP NetWeaver BI 連線類型](sap-netweaver-bi-connection-type-ssrs.md)|SAP NetWeaver BI|  
|[Hyperion Essbase 連線類型 &#40;SSRS&#41;](hyperion-essbase-connection-type-ssrs.md)|Hyperion Essbase|  
|[OLE DB &#40;SSRS&#41;的連線類型](ole-db-connection-type-ssrs.md)|OLE DB|  
|[ODBC 連線類型 &#40;SSRS&#41;](odbc-connection-type-ssrs.md)|ODBC|  
|[XML 連接類型 &#40;SSRS&#41;](xml-connection-type-ssrs.md)|XML|  

## <a name="Related"></a>相關章節  

本文件集的這些章節會提供報表資料的深入概念性資訊，以及如何定義、自訂和使用與報表資料相關組件的程序資訊。  

|主題|描述|  
|-----------|-----------------|  
|[將資料加入報表 &#40;報表產生器和 SSRS&#41;](report-datasets-ssrs.md)|提供存取報表資料的概觀。|  
|[報表產生器中的資料連接、資料來源及連接字串](../data-connections-data-sources-and-connection-strings-in-report-builder.md)|提供資料連接與資料來源的相關資訊。|  
|[報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)|提供內嵌與共用資料集的相關資訊。|  
|[資料集欄位集合 &#40;報表產生器及 SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)|提供查詢所產生之資料集欄位集合的相關資訊。|  
|《 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [線上叢書》](https://go.microsoft.com/fwlink/?linkid=121312)中檔集[Reporting Services &#40;SSRS&#41;支援的資料來源](../create-deploy-and-manage-mobile-and-paginated-reports.md)。|提供支援每一個資料延伸模組之平台與版本的深入資訊。|  
|《 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [線上叢書》](https://go.microsoft.com/fwlink/?linkid=121312)中檔[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]集的[資料處理延伸模組總覽](../extensions/data-processing/data-processing-extensions-overview.md)。|為進階使用者提供資料延伸模組的深入資訊。|  

## <a name="see-also"></a>另請參閱  

- [將資料加入報表 &#40;報表產生器和 SSRS&#41;](report-datasets-ssrs.md)
- [查詢設計工具 &#40;報表產生器&#41;](../query-designers-report-builder.md)