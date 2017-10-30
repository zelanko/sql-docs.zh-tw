---
title: "適用於 Microsoft Excel 的 Master Data Services 增益集 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/25/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 33d9c8fc-9602-494d-b9ab-8f0f42785974
caps.latest.revision: 30
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 07ec9e7ae52bb7adb85c2908c4b9b6da87e6ab19
ms.contentlocale: zh-tw
ms.lasthandoff: 09/07/2017

---
# <a name="master-data-services-add-in-for-microsoft-excel"></a>適用於 Microsoft Excel 的 Master Data Services 增益集
  透過 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]，您可以將資料的篩選清單從 MDS 載入 Excel 中，以便將它當做任何其他資料使用。 完成之後，您可以將資料發行回 MDS，以便進行集中儲存。 安全性會決定您可以檢視和更新的資料。  
  
 [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] 如果您是管理員，請使用  來建立實體和屬性並且載入資料。 這樣就不需要使用任何其他工具，將資料載入模型中。  
  
 在 [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]中，您可以使用 Data Quality Services (DQS)，在將資料載入 MDS 之前比對資料。 這樣有助於防止 MDS 中的資料重複。  

## <a name="downloads"></a>下載 
>*  從[此 Microsoft 下載中心頁面](https://go.microsoft.com/fwlink/?linkid=836866)下載適用於 Excel 的 SQL Server 2016 SP1 Master Data Services 增益集。 
>* 從[此 Microsoft 下載中心頁面](https://go.microsoft.com/fwlink/?linkid=836867)下載適用於 SQL Server 2017 CTP1 的 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]。 此增益集也適用於 SQL Server 2017 RC1。

 
  
## <a name="terms"></a>詞彙  
 使用此增益集時，您可能會遇到下列詞彙。 如需這些概念的詳細資訊，請參閱 [Master Data Services 概觀 &#40;MDS&#41;](../../master-data-services/master-data-services-overview-mds.md)。  
  
-   *MDS repository* 是指儲存所有主要資料的位置。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 它是設定為儲存 MDS 資料的  資料庫。 若要使用儲存機制中的資料，您必須將資料載入 Excel 中。使用完成之後，您必須將變更發行回儲存機制。 管理員可以將新的實體和屬性加入至儲存機制。  
  
-   *MDS-managed data* 是指儲存在 MDS 儲存機制中而且您載入 Excel 中的資料，而這項資料會顯示成反白顯示的資料列。 您可以將非 MDS 管理的資料加入至工作表，而且這項資料在您重新整理 MDS 管理的資料時不受影響。  
  
-   *model* 是指資料的容器。 您可以建立這些容器的版本，而且通常最新版本就是最近使用的版本。 如需詳細資訊，請參閱[模型 &#40;Master Data Services&#41;](../../master-data-services/models-master-data-services.md)。  
  
-   *entity* 是指資料的清單。 您可以將實體視為資料庫中的資料表。  例如，Color 實體可能會包含色彩的清單。 如需詳細資訊，請參閱[實體 &#40;Master Data Services&#41;](../../master-data-services/entities-master-data-services.md)。  
  
-   「成員」是指資料列 (記錄)。 每個實體都包含成員。 **Blue**是成員的範例。 如需詳細資訊，請參閱[成員 &#40;Master Data Services&#41;](../../master-data-services/members-master-data-services.md)。  
  
-   *attribute* 是指資料行。 每個成員都具有屬性。 例如，**Blue** 成員的 **Code** 屬性是 **B**。如需屬性的詳細資訊，請參閱[屬性 &#40;Master Data Services&#41;](../../master-data-services/attributes-master-data-services.md)。  
  
## <a name="related-tasks"></a>相關工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 建立  儲存機制的連接。|[連接到 MDS 存放庫 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/connect-to-an-mds-repository-mds-add-in-for-excel.md)|  
|將 MDS 管理的資料載入 Excel 中。|[將資料從 Master Data Services 匯出至 Excel](../../master-data-services/microsoft-excel-add-in/export-data-to-excel-from-master-data-services.md)|  
|儲存捷徑查詢，讓您日後可以用來開啟目前顯示之 MDS 管理的資料。|[儲存捷徑查詢檔案 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/save-a-shortcut-query-file-mds-add-in-for-excel.md)|  
|與其他人共用捷徑。|[以電子郵件傳送捷徑查詢檔案 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/email-a-shortcut-query-file-mds-add-in-for-excel.md)|  
|檢視已經對成員進行的所有變更。|[檢視成員的所有註解或交易 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/view-all-annotations-or-transactions-for-a-member-mds-add-in-for-excel.md)|  
|發行新資料之前，了解是否有重複。|[比對相似資料 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/match-similar-data-mds-add-in-for-excel.md)|  
|將資料從工作表發行到 MDS 儲存機制。|[將資料從 Excel 匯入 Master Data Services &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)|  
|使用工作表中的資料來建立新的實體。 (僅限管理員)|[建立實體 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/create-an-entity-mds-add-in-for-excel.md)|  
|建立網域屬性，也稱為受條件約束的清單。 (僅限管理員)|[建立網域屬性 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/create-a-domain-based-attribute-mds-add-in-for-excel.md)|  
|設定在適用於 Excel 的 Master Data Services 增益集中載入與發行資料的屬性。 (僅限管理員)|[設定適用於 Excel 之 Master Data Services 增益集的屬性](../../master-data-services/microsoft-excel-add-in/setting-properties-for-master-data-services-add-in-for-excel.md)|  
  
## <a name="related-content"></a>相關內容  
  
-   [連接 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/connections-mds-add-in-for-excel.md)  
  
-   [概觀：將資料匯出至 Excel &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/overview-exporting-data-to-excel-mds-add-in-for-excel.md)  
  
-   [捷徑查詢檔案 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/shortcut-query-files-mds-add-in-for-excel.md)  
  
-   [重新整理資料 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/refreshing-data-mds-add-in-for-excel.md)  
  
-   [概觀：從 Excel 匯入資料 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
-   [驗證資料 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/validating-data-mds-add-in-for-excel.md)  
  
-   [適用於 Excel 的 MDS 增益集中的資料品質比對](../../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md)  
  
-   [建立模型 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/building-a-model-mds-add-in-for-excel.md)  
  
-   [設定適用於 Excel 之 Master Data Services 增益集的屬性](../../master-data-services/microsoft-excel-add-in/setting-properties-for-master-data-services-add-in-for-excel.md)  
  
-   [安全性 &#40;Master Data Services&#41;](../../master-data-services/security-master-data-services.md)  
  
  

