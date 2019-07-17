---
title: 評估的整備程度移轉至 Azure SQL Database 的 SQL Server 資料資產 |Microsoft Docs
description: 了解如何使用 Data Migration Assistant 將移轉的 SQL Server 資料資產移轉至 Azure SQL Database
ms.custom: ''
ms.date: 07/16/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, on-premises SQL Server
ms.assetid: ''
author: HJToland3
ms.author: rajpo
manager: jroth
ms.openlocfilehash: d317fb3f0c2227744318eeaead71514095afbdec
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/16/2019
ms.locfileid: "68269380"
---
# <a name="assess-the-readiness-of-a-sql-server-data-estate-migrating-to-azure-sql-database-using-the-data-migration-assistant"></a>評估 SQL Server 資料的項目，移轉到 Azure SQL Database 使用 Data Migration Assistant

移轉 SQL Server 執行個體的上百和上千個資料庫移轉至 Azure SQL Database，我們的平台即服務 (PaaS) 供應項目，是相當大的工作。 為了簡化最大的處理程序，您需要您相對做好移轉自信。 識別省錢，包括伺服器和資料庫就緒，或需要最少的工作，以準備移轉、 簡化和加速您的工作。

本文提供逐步指示，以便能運用[Data Migration Assistant](https://docs.microsoft.com/sql/dma/dma-overview?view=sql-server-2017)彙總就緒結果和它們出現在[Azure Migrate](https://portal.azure.com/?feature.customPortal=false#blade/Microsoft_Azure_Migrate/AmhResourceMenuBlade/overview)中樞。

## <a name="create-a-project-and-add-a-tool"></a>建立專案，並加入工具

設定的 Azure 訂用帳戶中的新 Azure Migrate 專案，並新增一項工具。

Azure Migrate 專案用來儲存探索、 評估和移轉從您正在評估或移轉的環境收集的中繼資料。 若要追蹤已探索到的資產，並協調評定及移轉時，也可以使用專案。

1. 登入 Azure 入口網站中，選取**所有服務**，然後搜尋 Azure Migrate。
2. 底下**Services**，選取**Azure Migrate**。

   ![Azure Migrate-選取的服務](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-services.png)

3. 在 **概觀**頁面上，選取**評定，移轉資料庫**。

   ![Azure Migrate-起始評估](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-hub-assess.png)

4. 在**資料庫**下方**入門**，選取**新增工具**。

   ![Azure Migrate-新增工具](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-add-tools.png)

5. 在 **移轉專案**索引標籤上，選取您的 Azure 訂用帳戶和資源群組 （如果您還沒有資源群組中，建立一個）。
6. 底下**專案的詳細資料**，指定專案名稱和地理位置，且您想在其中建立專案。

    ![Azure Migrate-加入 [工具] 對話方塊](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-add-tool-dialog.png)

    您可以在任何這些地理位置中建立 Azure Migrate 專案。

    | **地理位置**  | **儲存體位置的區域** |
    | ------------- | ------------- |
    | 亞太地區 | 東南亞或東亞 |
    | Europe | 南歐或西歐 |
    | United Kingdom | 英國南部或英國西部 |
    | United States | 美國中部 」 或 「 美國西部 2 |

    指定給專案的地理只用來儲存從內部部署 Vm 收集來的中繼資料。 您可以選取任何實際移轉的目標區域。

7. 選取 [**下一步]** ，然後新增評估工具。

   > [!NOTE]
   > 當您建立專案時，您必須新增至少一個評定或移轉的工具。

8. 在 **選取評估工具**索引標籤上， **Azure Migrate:部署資料庫評估**會顯示為 「 評估 」 工具來加入。 如果您目前不需要評估工具，請選取**略過加入評估工具現在**核取方塊。 選取 [下一步]  。

    ![Azure Migrate-選取的評量工具索引標籤](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-select-assessment-tool.png)

9. 在 **選取的移轉工具**索引標籤上， **Azure Migrate:資料庫移轉**作為移轉工具，將會出現。 如果您目前不需要移轉工具，請選取**略過加入目前的移轉工具**。 選取 [下一步]  。

    ![Azure Migrate-選取的移轉工具 索引標籤](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-select-migration-tool.png)

10. 在 **檢閱 + 新增工具**，檢閱設定，然後選取**將工具新增**。

    ![Azure Migrate-檢閱 + 加入工具 索引標籤](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-review-tools.png)

    建立專案之後，您可以選取評定及移轉的伺服器和工作負載、 資料庫和 web 應用程式的其他工具。

## <a name="assess-and-upload-assessment-results"></a>評估並上傳評估結果

您已成功建立移轉專案，在後**評量工具**，請在**Azure Migrate:部署資料庫評估**方塊中，下載並使用 Data Migration Assistant 工具顯示的指示。

   ![Azure Migrate-新增的評估工具](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-assessment-tool-added.png)

1. 下載 Data Migration Assistant 使用提供的連結，然後將它安裝在您的來源 SQL Server 執行個體存取的電腦。
2. 啟動 Data Migration Assistant。

### <a name="create-an-assessment"></a>建立評定

1. 在左側，選取 **+** 圖示，然後再選取評估**專案類型**
2. 指定專案名稱，然後再選取目標伺服器類型與來源伺服器。

    如果至較新版的 SQL Server 或裝載於 Azure VM 上的 SQL Server，您要升級您的內部部署 SQL Server 執行個體，將來源和目標伺服器類型設為**SQL Server**。 若要設定目標伺服器類型**Azure SQL Database 受控執行個體**for Azure SQL Database (PaaS) 目標整備性評估。

3. 選取 [建立]  。

   ![Azure Migrate-Data Migration Assistant 介面](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-interface.png)

### <a name="choose-assessment-options"></a>選擇評估選項

1. 選取報表類型。

    您可以選擇其中一個或多個下列報表類型：
    * 檢查資料庫相容性
    * 檢查功能同位

   ![Azure Migrate-Data Migration Assistant-評定選項畫面](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-options-screen.png)

2. 選取 [下一步]  。

### <a name="add-databases-to-assess"></a>新增資料庫以評估

1. 選取 **加入來源**若要開啟 連接即時縮小功能表。
2. 輸入 SQL server 執行個體名稱、 選擇驗證類型、 設定正確的連接屬性，然後按**Connect**。
3. 選取的資料庫，以評估，然後選取**新增**。

   > [!NOTE]
   > 您可以移除多個資料庫，方法是選取它們時按住 Shift 或 Ctrl 鍵，，然後按一下 移除的來源。 您也可以使用 [新增來源] 按鈕，來新增多個 SQL Server 執行個體的資料庫。

4. 選取 [**下一步]** 以開始評估。

   ![Azure Migrate-資料移轉小幫手-選取來源畫面](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-select-sources-screen.png)

5. 評估完成之後，請選取**上傳至 Azure Migrate**。

   ![Azure Migrate-資料移轉小幫手-檢閱結果 畫面](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-review-results-screen.png)

6. 登入 Azure 入口網站。

   ![Azure Migrate-資料移轉小幫手-檢閱結果 畫面](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-portal-signin.png)

7. 選取訂用帳戶和 Azure Migrate 專案的項目，其中您想要上傳的評估結果，然後按**上傳**。

   等候評估上傳確認。

## <a name="view-target-readiness-assessment-results"></a>檢視目標整備評估結果

1. 登入 Azure 入口網站，Azure migrate，搜尋並選取**Azure Migrate**。

   ![Azure Migrate-Azure 入口網站-服務搜尋](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-portal-search.png)

2. 選取 **評定，移轉資料庫**回到評定結果。

   ![Azure Migrate-檢閱評估結果](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-hub-assess.png)

    您可以檢視 SQL Server 就緒摘要，請確定您位於正確的移轉專案，使用的選項，以選取不同的移轉專案的變更，否則為。

    每次您更新至 Azure 的評估結果移轉專案，Azure migrate 中樞彙總所有結果，並提供摘要的報表。  您可以平行執行數個資料移轉小幫手評定，並將結果上傳至單一的移轉專案，以取得合併的整備 報表。

   ![Azure Migrate-檢閱完備性結果](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-review-readiness.png)

    **評估資料庫執行個體**:評估目前的 SQL Server 執行個體數目。
    **評估資料庫**:評估來評估的一或多個 SQL Server 執行個體之間的資料庫總數**資料庫可供 SQL DB**:準備好移轉到 Azure SQL Database (PaaS) 的資料庫數目。
    **資料庫可供 Azure SQL VM**:資料庫數目會包含一或多個移轉封鎖程式到 Azure SQL Database (PaaS)，但要移轉至 Azure SQL Server Vm。

3. 選取 **評估資料庫執行個體**移至 SQL Server 執行個體層級檢視。

   ![Azure Migrate-檢閱執行個體的整備程度](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-assessed-instances.png)

    您可以找到每個 SQL Server 執行個體移轉至 Azure SQL Database (PaaS) 的百分比整備狀態。

4. 選取 移至 資料庫移轉整備程度檢視特定執行個體。

   ![Azure Migrate-檢閱資料庫的整備程度](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-assessed-databases.png)

    您可以看到依每個資料庫，建議的目標，每個上述檢視中的每個資料庫的移轉封鎖器數目。

5. 檢閱 DMA 的評估結果，以取得有關移轉封鎖程式的更多詳細資料。

   ![Azure Migrate-檢閱移轉封鎖程式](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-migration-blockers.png)

## <a name="see-also"></a>另請參閱

* [Data Migration Assistant (DMA)](../dma/dma-overview.md)
* [資料移轉小幫手：組態設定](../dma/dma-configurationsettings.md)
* [資料移轉小幫手：最佳作法](../dma/dma-bestpractices.md)
