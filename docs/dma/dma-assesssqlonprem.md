---
title: 執行 SQL Server 移轉評估 （資料移轉小幫手） |Microsoft 文件
ms.custom: ''
ms.date: 10/04/2017
ms.prod: sql-non-specified
ms.prod_service: dma
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-dma
ms.tgt_pltfrm: ''
ms.topic: article
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1c23f8d37e7af9daad2af78164a21adbe8c613a3
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="perform-a-sql-server-migration-assessment"></a>執行 SQL Server 移轉評估
下列的逐步指示會協助您移轉至內部部署 SQL Server，使用資料移轉小幫手來執行在 Azure VM 或 Azure SQL Database 上的 SQL Server 的執行您的第一次評估。

## <a name="create-an-assessment"></a>建立評量

1.  選取**新增**（+） 圖示，然後選取**評估**專案類型。

2.  設定來源和目標伺服器類型。

    如果現代在內部部署 SQL Server 執行個體或裝載於 Azure VM 上的 SQL Server，您要升級您的內部部署 SQL Server 執行個體，將來源和目標伺服器類型設為**SQL Server**。 如果您要移轉至 Azure SQL Database，改為將目標伺服器類型設為**Azure SQL Database**。

3.  按一下 **[建立]**。

    ![建立評量](../dma/media/NewAssessment.png)

## <a name="choose-assessment-options"></a>選擇評估選項

1. 選取您要移轉至目標 SQL Server 版本。

2. 選取報表類型。

   當您要評估您的來源 SQL Server 執行個體移轉到內部部署 SQL Server 或 SQL Server 裝載於 Azure VM 的目標時，您可以選擇其中一個或多個下列評估報表類型：

    -   **相容性問題**

    -   **新功能的建議**

    ![選取 SQL Server 目標評估報表類型](../dma/media/AssessmentTypes.png)

   當您要評估您的來源 SQL Server 執行個體移轉到 Azure SQL Database 時，您可以選擇其中一個或多個下列評估報表類型：

    -   **資料庫相容性檢查**

    -   **檢查功能同位檢查**

    ![選取 SQL 資料庫目標的評估報告類型](../dma/media/AssessmentTypes_Azure.png)

## <a name="add-databases-to-assess"></a>新增資料庫以評估

1.  選取**加入來源**開啟連接彈出式視窗功能表。

2.  輸入 SQL server 執行個體名稱，選擇 驗證類型、 設定正確的連接屬性，然後選取**連接**。

3.  選取的資料庫來評估，然後選取**新增**。

    > [!NOTE] 
    > 您可以同時按住 Shift 或 Ctrl 鍵，然後按一下即可移除多個資料庫**移除來源**。 您也可以加入多個 SQL Server 執行個體從資料庫，使用**加入來源** 按鈕。

4.  按一下**下一步**開始評估。

    ![加入來源，並開始評估](../dma/media/SelectDatabase.png)

## <a name="view-results"></a>檢視結果

評估的持續時間取決於新增的資料庫數目和每個資料庫的結構描述的大小。 可供使用時，結果會顯示每個資料庫。

1.  選取的資料庫，已完成評估，然後間進行切換**相容性問題**和**功能建議**使用切換器。

2.  檢閱相容性問題的所有相容性層級目標 SQL Server 版本所支援您在選取**選項**頁面。

您可以藉由分析受影響的物件和其識別在每個問題的詳細資料檢閱相容性問題**重大變更**，**行為變更**，和**已被取代功能**.

![檢視評估結果](../dma/media/ReviewResults.png)

同樣地，您可以檢閱跨功能建議**效能**，**儲存體**，和**安全性**區域。

功能建議涵蓋各種功能，例如記憶體內部 OLTP 和資料行存放區，Stretch Database，永遠加密，動態資料遮罩，以及透明資料加密。

![檢視功能建議](../dma/media/FeatureRecommendations.png)

Azure SQL database，評估會提供移轉封鎖問題和功能同位檢查問題。 選取特定的選項，以檢閱這兩種類別的結果。

- **SQL Server 功能同位檢查**類別提供一組完整的建議，可在 Azure 中和補救步驟的替代方法。 它可協助您規劃在移轉專案中的這項工作。

  ![檢視 SQL Server 功能同位檢查的資訊](../dma/media/SQLFeatureParity.png)

- **相容性問題**類別提供封鎖在內部部署 SQL Server 資料庫移轉至 Azure SQL database 的部分支援或不受支援的功能。 然後，它會提供建議，協助您解決這些問題。

  ![檢視相容性問題](../dma/media/CompatibilityIssues.png)

## <a name="export-results"></a>匯出結果

所有資料庫都完成評估之後，請選取**將報表匯出**，將結果匯出至 JSON 檔案或 CSV 檔案。 您可以在自己的方便分析資料。

您可以同時執行多個評估，並開啟檢視的評估狀態**所有評估**頁面。
