---
title: 執行 SQL Server 移轉評估 (Data Migration Assistant) |Microsoft Docs
description: 了解如何使用 Data Migration Assistant 評估內部部署 SQL Server 移轉至另一個 SQL Server 或 Azure SQL Database 之前
ms.custom: ''
ms.date: 10/04/2017
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
ms.openlocfilehash: bfb92c1217fe95687bdef5203189315b965b7446
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/04/2018
ms.locfileid: "37782219"
---
# <a name="perform-a-sql-server-migration-assessment-with-data-migration-assistant"></a>執行 SQL Server 移轉評估，使用 Data Migration Assistant

下列的逐步指示可協助您移轉至內部部署 SQL Server，使用 Data Migration Assistant 的 Azure VM 或 Azure SQL Database 上執行的 SQL Server 執行您的第一次評估。

## <a name="create-an-assessment"></a>建立評定

1.  選取 **的新**（+） 圖示，然後再選取**評定**專案類型。

2.  設定來源和目標伺服器類型。

    現代化內部部署 SQL Server 執行個體或裝載於 Azure VM 上的 SQL Server，您要升級您的內部部署 SQL Server 執行個體，如果來源和目標伺服器類型設為**SQL Server**。 如果您要移轉至 Azure SQL Database，而是會將目標伺服器類型設為**Azure SQL Database**。

3.  按一下 **[建立]**。

    ![建立評定](../dma/media/NewAssessment.png)

## <a name="choose-assessment-options"></a>選擇評估選項

1. 選取您打算移轉至目標 SQL Server 版本。

2. 選取報表類型。

   當您要評估您的來源 SQL Server 執行個體移轉至內部部署 SQL Server 或 SQL Server 裝載於 Azure VM 的目標時，您可以選擇其中一個或多個下列的評估報告類型：

    -   **相容性問題**

    -   **新功能的建議**

    ![選取 SQL Server 目標評估報表類型](../dma/media/AssessmentTypes.png)

   當您要評估您的來源 SQL Server 執行個體移轉到 Azure SQL Database 時，您可以選擇其中一個或多個下列的評估報告類型：

    -   **檢查資料庫相容性**

    -   **檢查功能同位**

    ![選取 SQL Database 目標的評估報告類型](../dma/media/AssessmentTypes_Azure.png)

## <a name="add-databases-to-assess"></a>新增資料庫以評估

1.  選取 **加入來源**以開啟 連線 飛出視窗功能表。

2.  輸入 SQL server 執行個體名稱、 選擇驗證類型、 設定正確的連接屬性，然後按**Connect**。

3.  選取的資料庫，以評估，然後選取**新增**。

    > [!NOTE] 
    > 您可以移除多個資料庫，方法是選取它們時按住 Shift 或 Ctrl 鍵，然後再按一下**移除來源**。 您也可以新增多個 SQL Server 執行個體的資料庫，使用**加入來源** 按鈕。

4.  按一下 [**下一步]** 以開始評估。

    ![新增來源，並啟動評量](../dma/media/SelectDatabase.png)

## <a name="view-results"></a>檢視結果

評估的持續時間取決於新增的資料庫數目和每個資料庫的結構描述的大小。 一旦可供使用，結果會顯示每個資料庫。

1.  選取的資料庫，已完成評估，並切換**相容性問題**並**功能建議**使用切換器。

2.  檢閱跨所有相容性層級目標 SQL Server 版本支援您在選取的相容性問題**選項**頁面。

您可以藉由分析受影響的物件和其下識別每個問題的詳細資料檢閱相容性問題**重大變更**，**行為變更**，和**已淘汰的功能**.

![檢視評估結果](../dma/media/ReviewResults.png)

同樣地，您可以檢閱跨功能建議**效能**，**儲存體**，並**安全性**區域。

功能建議涵蓋各種不同的功能，例如記憶體內部 OLTP 和資料行存放區、 Stretch Database、 Always Encrypted、 動態資料遮罩和透明資料加密。

![檢視功能建議](../dma/media/FeatureRecommendations.png)

針對 Azure SQL Database，評估會提供阻礙移轉的問題和功能同位問題。 選取特定的選項來檢閱這兩種類別的結果。

- **SQL Server 功能同位**類別提供一組完整的建議，Azure，以及補救步驟中可用的替代方法。 它可協助您規劃在移轉專案中的這項工作。

  ![檢視 SQL Server 功能同位資訊](../dma/media/SQLFeatureParity.png)

- **相容性問題**類別提供封鎖在內部部署 SQL Server 資料庫移轉至 Azure SQL database 的部分支援或不受支援的功能。 然後，它會提供建議來協助您解決這些問題。

  ![檢視相容性問題](../dma/media/CompatibilityIssues.png)

## <a name="export-results"></a>匯出結果

所有資料庫都完成評估之後，請選取**將報表匯出**結果匯出至 JSON 檔案或 CSV 檔案。 您可以依您自己的方便分析資料。

您可以同時執行多個評估，並開啟檢視這些評估的狀態**所有評定**頁面。
