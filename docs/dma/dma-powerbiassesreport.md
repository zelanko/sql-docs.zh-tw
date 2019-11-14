---
title: 使用 Power BI 分析合併的評估報告
titleSuffix: Data Migration Assistant
description: 瞭解如何使用 Power BI 來分析已匯入及合併的資料移轉評量報告 SQL Server
ms.custom: seo-lt-2019
ms.date: 03/12/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: HJToland3
ms.author: rajpo
ms.openlocfilehash: f2385914fc97fa8e118d871ddac6e0cdc9d49247
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056499"
---
# <a name="analyze-consolidated-assessment-reports-created-by-data-migration-assistant-with-power-bi"></a>使用 Power BI 分析 Data Migration Assistant 所建立的匯總評量報告

本文說明如何建立 Power BI 報表來分析合併的遷移評量。

如需有關合併 Data Migration Assistant 所建立之遷移評量的詳細資訊，請參閱[合併評量報告](../dma/dma-consolidatereports.md)。

## <a name="sample-power-bi-reports"></a>範例 Power BI 報表

您可以從這個[GitHub 存放庫](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/data-migration-assistant)下載匯總遷移評量的 Power BI 報表範例。

其中包含下列報告： 

- [儀錶](#dashboard-report)

  包含快照統計資料和向下切入報表。

- [內部部署升級準備就緒](#on-premises-upgrade-readiness-report)

  資料來源是 DMAReporting 資料庫中的 UpgradeSuccessRanking 視圖。  此報告會顯示已評估資料庫的升級成功百分比。

- [內部部署功能同位](#on-premises-feature-parity-report)

  顯示目標 SQL Server 版本的功能建議。

- [Azure SQL DB 升級準備就緒](#azure-sql-db-upgrade-readiness-report)

  資料來源是 DMAReporting 資料庫中的 UpgradeSuccessRanking 視圖。  此報告會顯示針對 Azure SQL DB 遷移評估之資料庫的升級成功百分比。

- [Azure SQL DB 不支援的功能](#azure-sql-db-unsupported-features-report)

  顯示 Azure SQL DB （V12）中不支援之現有資料庫的功能。

您可以藉由變更 Power BI 中的資料來源，修改這些報表來與您的環境搭配使用。 

1. 選取 [**編輯查詢**] 旁的向下箭號，然後選取 [**資料來源設定**]。

   ![編輯查詢 功能表、 資料來源設定](../dma/media/DataSourceSettings.png)

1. 選取 [**變更來源 ...** ]，然後輸入伺服器和資料庫值。

   ![變更來源、伺服器和資料庫](../dma/media/ChangeSource.png)

1. 選取 **[確定]** ，然後選取 [**關閉**]。

1. 重新整理報表。

   ![重新整理 Power BI 報表](../dma/media/RefreshReport.png)

### <a name="dashboard-report"></a>儀表板報表

![儀表板報表](../dma/media/DashboardReport.png)

儀表板會顯示您所有評量的詳細資料。 您可以使用左側的交叉分析篩選器，依實例或資料庫進行篩選。 您可以使用橫條圖向下切入到特定的類別，以查看問題所在的位置。

若要向下切入，請選取橫條圖右上角有向下箭號的圓圈。

![類別深入分析](../dma/media/CategoryDrillDown.png)

如下圖所示（在 [**軸**] 底下）設定的明細序列。 若要變更順序，請將資料行拖曳至所需的順序。

![視覺效果，橫條圖軸](../dma/media/VisualizationsAxis.png)

當您第一次依特定資料庫進行篩選，然後向下切入至特定類別的問題時，此視圖會變得更強大。 在下列範例中，會選取 [實例**azfae-use-vm-sql01** ] 的 HR 資料庫，以查看防止進行遷移的所有物件（重大變更）。

![HR 資料庫的重大變更](../dma/media/BreakingChanges.png)

### <a name="on-premises-upgrade-readiness-report"></a>內部部署升級就緒狀態報表

![內部部署升級就緒狀態報表](../dma/media/OnPremisesUpgradeReadinessReport.png)

此報表會顯示您的資料庫如何準備好要遷移至較新版本的 SQL Server 的快照集。 這份報表中的資料來自 dbo。DMAReporting 資料庫中的 UpgradeSuccessFactor\_內部部署 view。

依實例和資料庫名稱進行篩選，以及使用頂端的計分卡時，您可以查看資料庫可能遷移的版本。 例如，如果您依 AdventureWorks 2012 資料庫進行篩選，您可以看到資料庫已準備好移至報表中列出的所有 SQL Server 版本。 這是由確保該資料庫和相容性層級沒有任何重大變更所決定。

![AdventureWorks 資料庫的升級成功因素](../dma/media/UpgradeSuccessFactor.png)

### <a name="on-premises-feature-parity-report"></a>內部部署功能同位報告

![內部部署功能同位報告](../dma/media/OnPremisesFeatureParityReport.png)

使用此報表來反白顯示目標 SQL Server 版本中可用於資料庫的新功能。

當您選取漏斗圖中的某項功能時，底部的資料會反白顯示哪些物件會受到該功能影響。 在下列範例中，已選取 [**儲存體節省量**] 功能的 Stretch database，並列出可受益于此功能的資料表。

![Stretch Database 的功能建議](../dma/media/FeatureRecommend_StretchDatabase.png)

### <a name="azure-sql-db-upgrade-readiness-report"></a>Azure SQL DB 升級就緒報告

![Azure SQL DB 升級就緒報告](../dma/media/AzureSQLDBUpgradeReadinessReport.png)

此報表顯示要遷移至 Azure SQL Database V12 的資料庫準備就緒。 這份報表中的資料來自 dbo。DMAReporting 資料庫中的 UpgradeSuccessRanking view。

### <a name="azure-features-parity-report"></a>Azure 功能同位報告

![Azure 功能同位報告](../dma/media/AzureFeaturesParityReport.png)

請使用這份報表來反白顯示 Azure SQL Database V12 不支援的*實例層級功能*。

當您選取漏斗圖中的功能時，底部的資料會列出不支援的實例和資料庫功能。 在下列範例中，選取了這項功能： **Azure SQL Database 中不支援 Always On 可用性群組**設定。  

![Always on 可用性群組功能](../dma/media/Feature_AlwaysOnAvailability.png)

 
### <a name="azure-sql-db-unsupported-features-report"></a>Azure SQL DB 不支援的功能報表

![Azure SQL DB 不支援的功能報表](../dma/media/AzureSQLDBUnsupportedFeaturesReport.png)

當目標為 Azure SQL Database （V12）時，此報表會反白顯示給定**資料庫**不支援的功能。

藉由依漏斗圖中的資料庫名稱和功能值進行篩選，您可以查看不支援功能的詳細資料。 詳細資料包括受影響的物件，以及解決問題的建議。

例如，無法升級 DTC 資料庫和**唯讀資料庫**的篩選，您可以查看受影響的物件清單。

![無法升級唯讀資料庫問題](../dma/media/ReadOnlyDatabases.png)

## <a name="see-also"></a>另請參閱

[Data Migration Assistant 總覽](../dma/dma-overview.md)

[Data Migration Assistant 下載](https://www.microsoft.com/download/details.aspx?id=53595)

[Power BI 下載](https://powerbi.microsoft.com/)
