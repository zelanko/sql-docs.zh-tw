---
title: 分析彙總的資料移轉小幫手評定報表，使用 Power BI (SQL Server) |Microsoft Docs
description: 了解如何使用 Power BI 來分析您已匯入，並合併 SQL Server 中的資料移轉評估報告
ms.custom: ''
ms.date: 09/07/2017
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.suite: sql
ms.technology: dma
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.openlocfilehash: dd2280fbc15ffe515cc8fc6b020a6ec3e2cf1647
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/04/2018
ms.locfileid: "37787629"
---
# <a name="analyze-consolidated-assessment-reports-created-by-data-migration-assistant-with-power-bi"></a>分析 Data Migration Assistant 有了 Power BI 所建立的彙總的評估報告

本文說明如何建立 Power BI 報告來分析合併的移轉評定。

如需彙總的資料移轉小幫手所建立的移轉評定資訊，請參閱[彙總評估報告](../dma/dma-consolidatereports.md)。

## <a name="sample-power-bi-reports"></a>範例 Power BI 報表

您可以從這個下載的彙總的移轉評定的 Power BI 報表範例[Github 存放庫](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/data-migration-assistant)。

包含下列報告︰ 

- [儀表板](#dashboard--details)

  包含快照集的統計資料和向下鑽研報表。

- [在內部部署環境更新整備小幫手](#on-premises-upgrade-readiness--details)

  資料來源是 UpgradeSuccessRanking 檢視 DMAReporting 資料庫中。  此報告會顯示您經過評定的資料庫百分比升級成功。

- [在內部部署功能同位檢查](#on-premise-feature-parity--details)

  顯示目標 SQL Server 版本的功能建議。

- [Azure SQL DB 更新整備小幫手](#azure-sql-db-upgrade-readiness--details)

  資料來源是 UpgradeSuccessRanking 檢視 DMAReporting 資料庫中。  此報告會顯示適用於 Azure SQL DB 移轉評估的資料庫百分比升級成功。

- [Azure SQL DB 不支援的功能](#azure-sql-db-unsupported-features--details)

  顯示您現有的資料庫不支援 Azure SQL DB (V12) 中的功能。

您可以修改這些報表來使用您的環境，藉由變更 Power BI 中的資料來源。 

1. 選取向下箭號旁**編輯查詢**，然後選取**資料來源設定**。

   ![編輯查詢] 功能表、 [資料來源設定](../dma/media/DataSourceSettings.png)

1. 選取**變更來源...**，然後輸入伺服器和資料庫的值。

   ![變更來源、 伺服器和資料庫](../dma/media/ChangeSource.png)

1. 選取  **確定**，然後選取**關閉**。

1. 重新整理您的報表。

   ![重新整理 Power BI 報表](../dma/media/RefreshReport.png)

### <a name="dashboard-report"></a>儀表板報表

![儀表板報表](../dma/media/DashboardReport.png)

儀表板會顯示所有您評量的詳細資料。 您可以使用左側的交叉分析篩選器，以篩選出的執行個體或資料庫。 您可以向下切入到特定的類別，以查看其中的問題也都必須位於使用橫條圖。

若要向下切入，選取與橫條圖的右上角的向下箭頭的圓圈。

![類別目錄向下鑽研](../dma/media/CategoryDrillDown.png)

向下鑽研順序設定在下圖所示 (底下**軸**)。 若要變更順序，將資料行拖曳至所需的順序。

![視覺效果時，橫條圖的軸](../dma/media/VisualizationsAxis.png)

當您第一次來篩選特定的資料庫，然後向下鑽研至特定分類問題時，此檢視會變得更強大。 在下列範例中，HR 資料庫執行個體已選取**SQL01**若要檢視的所有物件，使移轉 （重大變更）。

![HR 資料庫的重大變更](../dma/media/BreakingChanges.png)

### <a name="on-premises-upgrade-readiness-report"></a>在內部部署升級整備報表

![在內部部署升級整備報表](../dma/media/OnPremisesUpgradeReadinessReport.png)

此報告會顯示移轉到新版的 SQL Server 的 「 如何準備您的資料庫是快照集。 此報表中的資料來自於 dbo。UpgradeSuccessFactor\_DMAReporting 資料庫中的內部部署檢視。

使用頂端的計分卡和篩選的執行個體和資料庫名稱，您可以看到它可能太移轉資料庫的版本。 比方說，如果您篩選由 AdventureWorks 2012 資料庫時，您可以看到資料庫已準備好移至報表中列出的所有 SQL Server 版本。 這取決於確保沒有任何重大變更，該資料庫和相容性層級。

![升級成功的因素，針對 AdventureWorks 資料庫](../dma/media/UpgradeSuccessFactor.png)

### <a name="on-premises-feature-parity-report"></a>在內部部署功能同位檢查報表

![在內部部署功能同位檢查報表](../dma/media/OnPremisesFeatureParityReport.png)

您可以使用此報告來反白顯示可用的目標 SQL Server 版本中的資料庫的新功能。

當您在漏斗圖中選取一項功能時，在下方的資料會反白顯示哪些物件會受此功能。 在下列範例中， **Stretch database，以節省儲存空間**選取功能，且資料表會列出可能會受益於這項功能。

![Stretch Database 的功能建議](../dma/media/FeatureRecommend_StretchDatabase.png)

### <a name="azure-sql-db-upgrade-readiness-report"></a>Azure SQL DB 更新整備小幫手報告

![Azure SQL DB 更新整備小幫手報告](../dma/media/AzureSQLDBUpgradeReadinessReport.png)

此報告會顯示移轉至 Azure SQL Database V12 資料庫完備性。 這份報表的資料來自於 dbo。UpgradeSuccessRanking DMAReporting 資料庫中的檢視。

### <a name="azure-features-parity-report"></a>Azure 的功能同位檢查報告

![Azure 的功能同位檢查報告](../dma/media/AzureFeaturesParityReport.png)

使用此報告來反白顯示*執行個體層級的功能*，不支援的 Azure SQL Database V12。

當您在漏斗圖中選取一項功能時，在底端的資料會列出的執行個體和資料庫不支援的功能。 在下列範例中，選取這項功能： **Always on 可用性群組組態不支援 Azure SQL Database 中**。  

![Alwayson 可用性群組功能](../dma/media/Feature_AlwaysOnAvailability.png)

 
### <a name="azure-sql-db-unsupported-features-report"></a>Azure SQL DB 不支援的功能報告

![Azure SQL DB 不支援的功能報告](../dma/media/AzureSQLDBUnsupportedFeaturesReport.png)

此報表會反白顯示哪些功能不支援給定**資料庫**時的目標是 Azure SQL Database (V12)。

藉由篩選漏斗圖中的資料庫名稱與功能值，您可以查看不支援的功能的詳細資料。 詳細資料包括哪些物件會受影響及解決問題的建議。

例如，篩選由 DTC 資料庫並**無法升級唯讀資料庫**，您可以看到一份受影響的物件。

![唯讀資料庫不能升級問題](../dma/media/ReadOnlyDatabases.png)

## <a name="see-also"></a>另請參閱

[Data Migration Assistant 的概觀](../dma/dma-overview.md)

[資料移轉小幫手下載](https://www.microsoft.com/download/details.aspx?id=53595)

[Power BI 下載](https://powerbi.microsoft.com/)
