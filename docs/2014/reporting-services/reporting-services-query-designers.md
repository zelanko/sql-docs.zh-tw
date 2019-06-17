---
title: Reporting Services 查詢設計工具 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- query designers [Reporting Services]
ms.assetid: 07efd3f1-804f-45f7-b62a-3e727a3d9835
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c004b098f900606c2263391cf9363b6e5be2b97b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66102876"
---
# <a name="reporting-services-query-designers"></a>Reporting Services 查詢設計工具
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 提供圖形化和以文字為基礎的查詢設計工具，可協助您在報表中每個資料來源類型為建立查詢。  
  
 某些資料來源支援可協助您以互動方式建立查詢的圖形化設計工具。 其他資料來源則使用以文字為基礎的查詢設計工具。 利用圖形化查詢設計工具，您可以將資料來源上，表示基礎資料的中繼資料項目拖曳到查詢設計介面。 利用以文字為基礎的查詢設計工具，您可以將命令文字輸入到查詢窗格中。 您可以從圖形化查詢設計工具切換到以文字為基礎的查詢設計工具，方法是按一下工具列上以文字為基礎的查詢設計工具圖示。  
  
 報表中的可用資料來源類型取決於用戶端或報表伺服器上安裝的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 資料延伸模組。 如需詳細資訊，請參閱 < [RSReportDesigner Configuration File](report-server/rsreportdesigner-configuration-file.md)並[RSReportServer Configuration File](report-server/rsreportserver-config-configuration-file.md)。  
  
 資料處理延伸模組及其相關聯的查詢設計工具，在資料來源支援的下列方式可能會有不同：  
  
-   **依查詢設計工具類型。** 例如， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料來源同時支援圖形化查詢設計工具以及以文字為基礎的查詢設計工具。  
  
-   **依查詢語言變化。** 例如， [!INCLUDE[tsql](../includes/tsql-md.md)] 這類的查詢語言在語法上可能會視資料來源類型而有所不同。 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[tsql](../includes/tsql-md.md)] 語言和 Oracle SQL 語言在查詢命令的語法上有一些不同。  
  
-   **依資料庫物件名稱的結構描述部分支援。** 當資料來源使用結構描述做為資料庫物件識別碼的一部分時，必須針對不使用預設結構描述的任何名稱，提供結構描述名稱做為查詢的一部分。 例如， `SELECT FirstName, LastName FROM [Person].[Person]` 。  
  
-   **依查詢參數支援。** 資料提供者的差異在於參數的支援。 有些資料提供者支援指名參數，例如， `SELECT Col1, Col2 FROM Table WHERE <parameter identifier><parameter name> = <value>`。 有些資料提供者則支援未指名參數，例如， `SELECT Col1, Col2 FROM Table WHERE <column name> = ?`。 參數識別碼可能依資料提供者而有所不同，例如， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 使用 @ 符號，而 Oracle 使用冒號 (:)。 而有些資料提供者不支援參數。  
  
-   **依匯入查詢的能力。** 例如，若為 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料來源，您可以從報表定義檔案 (.rdl) 或 .sql 檔案匯入查詢。  
  
## <a name="query-designers"></a>查詢設計工具  
 下列主題會描述每一個查詢設計工具的使用者介面。  
  
-   [Analysis Services MDX 查詢設計工具使用者介面](report-data/analysis-services-mdx-query-designer-user-interface.md)  
  
-   [Analysis Services DMX 查詢設計工具使用者介面](report-data/analysis-services-dmx-query-designer-user-interface.md)  
  
-   [圖形化查詢設計工具使用者介面](report-data/graphical-query-designer-user-interface.md)  
  
-   [關聯式查詢設計工具使用者介面](../../2014/reporting-services/relational-query-designer-user-interface.md)  
  
-   [Hyperion Essbase 查詢設計工具使用者介面](report-data/hyperion-essbase-query-designer-user-interface.md)  
  
-   [報表模型查詢設計工具使用者介面](report-data/report-model-query-designer-user-interface.md)  
  
-   [SAP NetWeaver BI 查詢設計工具使用者介面](report-data/sap-netweaver-bi-query-designer-user-interface.md)  
  
-   [SharePoint 清單查詢設計工具](../../2014/reporting-services/sharepoint-list-query-designer.md)  
  
-   [以文字為基礎的查詢設計工具使用者介面](../../2014/reporting-services/text-based-query-designer-user-interface.md)  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services &#40;SSRS&#41; 支援的資料來源](create-deploy-and-manage-mobile-and-paginated-reports.md)   
 [從外部資料來源新增資料 &#40;SSRS&#41;](report-data/add-data-from-external-data-sources-ssrs.md)   
 [資料處理延伸模組與.NET Framework 資料提供者&#40;SSRS&#41;](report-data/data-processing-extensions-and-net-framework-data-providers-ssrs.md)   
 [延伸模組 &#40;SSRS&#41;](extensions-ssrs.md)  
  
  
