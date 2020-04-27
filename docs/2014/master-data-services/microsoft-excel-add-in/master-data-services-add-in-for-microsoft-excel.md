---
title: 適用於 Microsoft Excel 的 Master Data Services 增益集 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 33d9c8fc-9602-494d-b9ab-8f0f42785974
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: d8bac9ba8afafa6b5141d90c51f8029f596ba8f4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "65482619"
---
# <a name="master-data-services-add-in-for-microsoft-excel"></a>適用於 Microsoft Excel 的 Master Data Services 增益集
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]透過[!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]，可以將參考資料的主要清單散發給組織中使用 Excel 的每個人。 安全性會決定使用者可檢視和更新的資料。  
  
 您可以將資料的篩選清單從 MDS 載入 Excel 中，以便將它當做任何其他資料使用。 完成之後，您可以將資料發行回 MDS，以便進行集中儲存。  
  
 [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] 如果您是管理員，請使用  來建立實體和屬性並且載入資料。 這樣就不需要使用任何其他工具，將資料載入模型中。  
  
 在 [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]中，您可以使用 Data Quality Services (DQS)，在將資料載入 MDS 之前比對資料。 這樣有助於防止 MDS 中的資料重複。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 將 Master Data Services 和 Data Quality Services 升級為 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CTP2 之後，您可以繼續使用  SP1 版適用於 Excel 的 Master Data Services 增益集。 不過，在升級為 SQL Server 2014 CTP2 之後，任何舊版適用於 Excel 的 Master Data Services 增益集將無法運作。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 您可以在 [這裡](https://go.microsoft.com/fwlink/?LinkId=328664)下載  SP1 版適用於 Excel 的 Master Data Services 增益集。  
  
## <a name="terms"></a>詞彙  
 使用此增益集時，您可能會遇到下列詞彙。  
  
-   *MDS repository* 是指儲存所有主要資料的位置。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 它是設定為儲存 MDS 資料的  資料庫。 若要使用儲存機制中的資料，您必須將資料載入 Excel 中。使用完成之後，您必須將變更發行回儲存機制。 管理員可以將新的實體和屬性加入至儲存機制。  
  
-   *MDS-managed data* 是指儲存在 MDS 儲存機制中而且您載入 Excel 中的資料，而這項資料會顯示成反白顯示的資料列。 您可以將非 MDS 管理的資料加入至工作表，而且這項資料在您重新整理 MDS 管理的資料時不受影響。  
  
-   *model* 是指資料的容器。 您可以建立這些容器的版本，而且通常最新版本就是最近使用的版本。 如需詳細資訊，請參閱[模型 &#40;Master Data Services&#41;](../models-master-data-services.md)。  
  
-   *entity* 是指資料的清單。 您可以將實體視為資料庫中的資料表。 **** 例如，Color 實體可能會包含色彩的清單。 如需詳細資訊，請參閱[實體 &#40;Master Data Services&#41;](../entities-master-data-services.md)。  
  
-   *member* 是指資料列。 每個實體都包含成員。 **Blue**是成員的範例。 如需詳細資訊，請參閱[成員 &#40;Master Data Services&#41;](../members-master-data-services.md)。  
  
-   *attribute* 是指資料行。 每個成員都具有屬性。 例如， **Blue**成員的**Code**屬性是**B**。如需屬性的詳細資訊，請參閱[&#40;Master Data Services&#41;的屬性](../attributes-master-data-services.md)。  
  
## <a name="related-tasks"></a>相關工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 建立  儲存機制的連接。|[連接到 MDS 儲存機制 &#40;適用於 Excel 的 MDS 增益集&#41;](connect-to-an-mds-repository-mds-add-in-for-excel.md)|  
|將 MDS 管理的資料載入 Excel 中。|[將資料從 MDS 載入 Excel 中](export-data-to-excel-from-master-data-services.md)|  
|儲存捷徑查詢，讓您日後可以用來開啟目前顯示之 MDS 管理的資料。|[儲存捷徑查詢檔案 &#40;適用於 Excel 的 MDS 增益集&#41;](save-a-shortcut-query-file-mds-add-in-for-excel.md)|  
|與其他人共用捷徑。|[以電子郵件傳送捷徑查詢檔案 &#40;適用於 Excel 的 MDS 增益集&#41;](email-a-shortcut-query-file-mds-add-in-for-excel.md)|  
|檢視已經對成員進行的所有變更。|[檢視成員的所有註解或交易 &#40;適用於 Excel 的 MDS 增益集&#41;](view-all-annotations-or-transactions-for-a-member-mds-add-in-for-excel.md)|  
|發行新資料之前，了解是否有重複。|[比對相似資料 &#40;適用於 Excel 的 MDS 增益集&#41;](match-similar-data-mds-add-in-for-excel.md)|  
|將資料從工作表發行到 MDS 儲存機制。|[將 Excel 的資料發行至適用于 Excel 的 mds 增益集 &#40;&#41;](import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)|  
|使用工作表中的資料來建立新的實體。 (僅限管理員)|[建立實體 &#40;適用於 Excel 的 MDS 增益集&#41;](create-an-entity-mds-add-in-for-excel.md)|  
|建立網域屬性，也稱為受條件約束的清單。 (僅限管理員)|[建立網域屬性 &#40;適用於 Excel 的 MDS 增益集&#41;](create-a-domain-based-attribute-mds-add-in-for-excel.md)|  
|設定在適用於 Excel 的 Master Data Services 增益集中載入與發行資料的屬性。 (僅限管理員)|[設定適用於 Excel 之 Master Data Services 增益集的屬性](setting-properties-for-master-data-services-add-in-for-excel.md)|  
  
## <a name="related-content"></a>相關內容  
  
-   [連接 &#40;適用於 Excel 的 MDS 增益集&#41;](connections-mds-add-in-for-excel.md)  
  
-   [載入適用于 Excel 的 MDS 增益集&#41;的資料 &#40;](overview-exporting-data-to-excel-mds-add-in-for-excel.md)  
  
-   [捷徑查詢檔案 &#40;適用於 Excel 的 MDS 增益集&#41;](shortcut-query-files-mds-add-in-for-excel.md)  
  
-   [適用於 Excel 的 MDS 增益集中的資料品質比對](data-quality-matching-in-the-mds-add-in-for-excel.md)  
  
-   [發行資料 &#40;適用于 Excel 的 MDS 增益集&#41;](overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
-   [建立模型 &#40;適用於 Excel 的 MDS 增益集&#41;](building-a-model-mds-add-in-for-excel.md)  
  
-   [安全性 &#40;Master Data Services&#41;](../security-master-data-services.md)  
  
  
