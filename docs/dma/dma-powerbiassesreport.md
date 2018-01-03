---
title: "使用 Power BI （SQL Server 資料移轉小幫手） 報告合併評估 |Microsoft 文件"
ms.custom: 
ms.date: 09/07/2017
ms.prod: sql-non-specified
ms.prod_service: dma
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: sql-dma
ms.tgt_pltfrm: 
ms.topic: article
keywords: 
helpviewer_keywords: Data Migration Assistant, Assess
ms.assetid: 
caps.latest.revision: 
author: HJToland3
ms.author: jtoland
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 62f3ed0802a0a7570109bdae99151c8c6ce4fa01
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="report-on-your-consolidated-assessments-by-using-power-bi-data-migration-assistant"></a>使用 Power BI （資料移轉小幫手） 合併評估報告

本文說明如何建立彙總的移轉評估的 Power BI 報表。

依使用的資料移轉小幫手彙總是移轉評估的資訊，請參閱[合併 Assessment 報表](../dma/dma-consolidatereports.md)。

## <a name="sample-power-bi-reports"></a>範例 Power BI 報表

您可以從這個下載的合併的移轉評估的 Power BI 報表範例[Github 儲存機制](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/data-migration-assistant)。

下列報表會包含： 

- [儀表板](#dashboard--details)

  包含快照集的統計資料和向下鑽研報表。

- [在內部部署升級整備情況](#on-premises-upgrade-readiness--details)

  資料來源是 UpgradeSuccessRanking 檢視 DMAReporting 資料庫中。  此報告會顯示您評估資料庫百分比升級成功。

- [在內部部署功能同位檢查](#on-premise-feature-parity--details)

  顯示目標 SQL Server 版本的功能建議。

- [Azure SQL DB 升級整備程度](#azure-sql-db-upgrade-readiness--details)

  資料來源是 UpgradeSuccessRanking 檢視 DMAReporting 資料庫中。  此報告會顯示評估為 Azure SQL DB 移轉的資料庫百分比升級成功。

- [Azure SQL DB 不支援的功能](#azure-sql-db-unsupported-features--details)

  顯示在 Azure SQL DB (V12) 中不支援將現有資料庫中的功能。

您可以修改這些報表來處理您的環境變更 Power BI 中的資料來源。 

1. 選取向下箭號旁**編輯查詢**，然後選取**資料來源設定**。

   ![編輯查詢 功能表、 資料來源設定](../dma/media/DataSourceSettings.png)

1. 選取**變更來源...**，然後輸入的伺服器和資料庫的值。

   ![變更來源、 伺服器和資料庫](../dma/media/ChangeSource.png)

1. 選取**確定**，然後選取**關閉**。

1. 重新整理您的報表。

   ![重新整理 Power BI 報表](../dma/media/RefreshReport.png)

### <a name="dashboard-report"></a>儀表板報表

![儀表板報表](../dma/media/DashboardReport.png)

儀表板會顯示有關所有評估詳細資料。 您可以使用左側的交叉分析篩選器，以篩選出的執行個體或資料庫。 您可以向下鑽研至特定的類別，以查看問題的地方，使用橫條圖。

若要向下切入，選取與橫條圖的右上角的向下箭號的圓圈。

![類別目錄的向下鑽研](../dma/media/CategoryDrillDown.png)

向下鑽研順序設定下列影像所示 (下**軸**)。 若要變更順序，將資料行拖曳到預期的順序。

![視覺效果 橫條圖的軸](../dma/media/VisualizationsAxis.png)

當您首先來篩選出特定的資料庫，然後向下鑽研至特定分類問題時，此檢視會變得更強大。 在下列範例中，HR 資料庫執行個體已選取**SQL01**若要檢視的所有物件，使移轉 （最新變更）。

![重大變更的 HR 資料庫](../dma/media/BreakingChanges.png)

### <a name="on-premises-upgrade-readiness-report"></a>在內部部署升級整備報表

![在內部部署升級整備報表](../dma/media/OnPremisesUpgradeReadinessReport.png)

此報告會顯示移轉至較新版的 SQL Server 的方式準備您的資料庫是快照的集。 此報表中的資料來自 dbo。UpgradeSuccessFactor\_OnPrem DMAReporting 資料庫中的檢視。

篩選的執行個體和資料庫名稱，以及使用計分卡在頂端，您可以查看哪些版本可能太移轉資料庫。 比方說，如果您篩選 AdventureWorks 2012 資料庫，您可以看到的資料庫是否準備好移至報表中列出的所有 SQL Server 版本。 這取決於確保沒有任何重大變更，該資料庫和相容性層級。

![針對 AdventureWorks 資料庫的升級成功因素](../dma/media/UpgradeSuccessFactor.png)

### <a name="on-premises-feature-parity-report"></a>在內部部署功能同位檢查報表

![在內部部署功能同位檢查報表](../dma/media/OnPremisesFeatureParityReport.png)

使用這份報表來反白顯示可用的資料庫中的目標 SQL Server 版本的新功能。

當您在漏斗圖中選取一項功能時，底部資料會反白顯示哪些物件會受影響的功能。 在下列範例中， **Stretch database 的存放裝置節省**選取功能，而且列於表格可能會受益於這項功能。

![針對 Stretch Database 功能建議](../dma/media/FeatureRecommend_StretchDatabase.png)

### <a name="azure-sql-db-upgrade-readiness-report"></a>Azure SQL DB 升級整備報表

![Azure SQL DB 升級整備報表](../dma/media/AzureSQLDBUpgradeReadinessReport.png)

此報告會顯示移轉到 Azure SQL Database V12 資料庫整備。 這份報表的資料來自 dbo。UpgradeSuccessRanking DMAReporting 資料庫中的檢視。

### <a name="azure-features-parity-report"></a>Azure 的功能同位檢查報告

![Azure 的功能同位檢查報告](../dma/media/AzureFeaturesParityReport.png)

使用此報表來反白顯示*執行個體層級功能*不由 Azure SQL Database V12 支援。

當您在漏斗圖中選取一項功能時，底部資料會列出執行個體和資料庫不支援的功能。 在下列範例中，選取此功能： **Azure SQL Database 不支援 Alwayson 可用性群組組態**。  

![Alwayson 可用性群組功能](../dma/media/Feature_AlwaysOnAvailability.png)

 
### <a name="azure-sql-db-unsupported-features-report"></a>Azure SQL DB 不支援的功能報告

![Azure SQL DB 不支援的功能報告](../dma/media/AzureSQLDBUnsupportedFeaturesReport.png)

此報表會反白顯示的功能不適用於給定**資料庫**當目標是 Azure SQL Database (V12)。

藉由篩選漏斗圖中的資料庫名稱和功能值，您可以查看詳細資料上不支援的功能。 詳細資料包含哪些物件會受影響和解決問題的建議。

例如，篩選由 DTC 資料庫和**無法升級唯讀資料庫**，您可以檢視受影響的物件清單。

![唯讀資料庫不能升級問題](../dma/media/ReadOnlyDatabases.png)

## <a name="see-also"></a>另請參閱

[資料移轉小幫手的概觀](../dma/dma-overview.md)

[資料移轉小幫手下載](https://www.microsoft.com/download/details.aspx?id=53595)

[Power BI 下載](https://powerbi.microsoft.com/)
