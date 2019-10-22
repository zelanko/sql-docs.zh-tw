---
title: 評估遷移至 Azure SQL Database 的 SQL Server 資料資產是否就緒 |Microsoft Docs
description: 瞭解如何使用 Data Migration Assistant 遷移 SQL Server 資料資產, 以供遷移至 Azure SQL Database
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
ms.openlocfilehash: b3f47cee5cc091c52faa98438d22b88a18a06f03
ms.sourcegitcommit: e821cd8e5daf95721caa1e64c2815a4523227aa4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/01/2019
ms.locfileid: "68702827"
---
# <a name="assess-the-readiness-of-a-sql-server-data-estate-migrating-to-azure-sql-database-using-the-data-migration-assistant"></a>使用 Data Migration Assistant, 評估遷移至 Azure SQL Database 的 SQL Server 資料資產是否就緒

將數百個 SQL Server 實例和上千個資料庫移轉至 Azure SQL Database (我們的平臺即服務 (PaaS) 供應專案) 是相當可觀的工作。 若要盡可能簡化此程式, 您必須安心瞭解您的相對就緒性以進行遷移。 識別低度的水果, 包括已完全準備就緒或需要最少準備進行遷移的伺服器和資料庫, 讓您的工作更輕鬆且更快。

這篇文章提供逐步指示, 說明如何利用[Data Migration Assistant](https://docs.microsoft.com/sql/dma/dma-overview?view=sql-server-2017)來總結準備就緒結果, 並在[Azure Migrate](https://portal.azure.com/?feature.customPortal=false#blade/Microsoft_Azure_Migrate/AmhResourceMenuBlade/overview)中樞上加以呈現。


> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Data-Migration-Assistant/player?WT.mc_id=dataexposed-c9-niner]

## <a name="create-a-project-and-add-a-tool"></a>建立專案並新增工具

在 Azure 訂用帳戶中設定新的 Azure Migrate 專案, 然後新增工具。

Azure Migrate 專案用來儲存從您要評估或遷移的環境中收集到的探索、評估和遷移中繼資料。 您也可以使用專案來追蹤探索到的資產, 並協調評估和遷移。

1. 登入 Azure 入口網站, 選取 [**所有服務**], 然後搜尋 Azure Migrate。
2. 在 [**服務**] 下, 選取 [ **Azure Migrate**]。

   ![Azure Migrate-選取服務](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-services.png)

3. 在 [**總覽**] 頁面上, 選取 [**評估和遷移資料庫**]。

   ![Azure Migrate-起始評估](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-hub-assess.png)

4. 在 [**資料庫**] 的 [使用者**入門**] 底下, 選取 **[新增工具**]。

   ![Azure Migrate-新增工具](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-add-tools.png)

5. 在 [**遷移專案**] 索引標籤上, 選取您的 Azure 訂用帳戶和資源群組 (如果您還沒有資源群組, 請建立一個)。
6. 在 [**專案詳細資料**] 下, 指定要在其中建立專案的專案名稱和地理位置。

    ![Azure Migrate-新增工具對話方塊](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-add-tool-dialog.png)

    您可以在這些地理區域中建立 Azure Migrate 專案。

    | **地理位置**  | **儲存位置區域** |
    | ------------- | ------------- |
    | Asia | 東南亞或東亞 |
    | Europe | 歐洲南部或西歐 |
    | United Kingdom | 英國南部或英國西部 |
    | United States | 美國中部或美國西部2 |

    針對專案所指定的地理位置只會用來儲存從內部部署 Vm 收集的中繼資料。 您可以選取任何目的地區域以進行實際的遷移。

7. 選取 **[下一步]** , 然後新增評估工具。

   > [!NOTE]
   > 當您建立專案時, 您必須加入至少一個評估或遷移工具。

8. 在 [**選取評估工具**] 索引**標籤上, Azure Migrate:資料庫評估**會顯示為要新增的評估工具。 如果您目前不需要評估工具, 請選取 [**立即略過新增評估工具**] 核取方塊。 選取 [下一步]。

    ![Azure Migrate-選取 [評估工具] 索引標籤](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-select-assessment-tool.png)

9. 在 [**選取遷移工具**] 索引**標籤上, Azure Migrate:資料庫移轉**會顯示為要新增的遷移工具。 如果您目前不需要遷移工具, 請選取 [**立即略過新增遷移工具**]。 選取 [下一步]。

    ![Azure Migrate-選取 [遷移工具] 索引標籤](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-select-migration-tool.png)

10. 在 [審核] 和 [**新增工具**] 中, 檢查設定, 然後選取 [**新增工具**]。

    ![Azure Migrate-審查 + 新增工具 索引標籤](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-review-tools.png)

    建立專案之後, 您可以選取其他工具來評估和遷移伺服器和工作負載、資料庫和 web 應用程式。

## <a name="assess-and-upload-assessment-results"></a>評估和上傳評估結果

成功建立遷移專案之後, 在 **評估工具** 底下的  **Azure Migrate:資料庫**評估 方塊中, 下載和使用 Data Migration Assistant 工具顯示的指示。

   ![已新增 Azure Migrate 評量工具](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-assessment-tool-added.png)

1. 使用提供的連結下載 Data Migration Assistant, 然後將它安裝在可存取來源 SQL Server 實例的電腦上。
2. 啟動 Data Migration Assistant。

### <a name="create-an-assessment"></a>建立評量

1. 在左側選取 **+** 圖示, 然後選取 [評估]**專案類型**
2. 指定 [專案名稱], 然後選取 [來源伺服器] 和 [目標伺服器類型]。

    如果您要將內部部署 SQL Server 實例升級至較新版本的 SQL Server 或裝載在 Azure VM 上的 SQL Server, 請將來源和目標伺服器類型設定為 [ **SQL Server**]。 將 目標伺服器類型 設定為 Azure SQL Database (PaaS) 目標就緒評量的**Azure SQL Database 受控執行個體**。

3. 選取 [建立]。

   ![Azure Migrate Data Migration Assistant 介面](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-interface.png)

### <a name="choose-assessment-options"></a>選擇評量選項

1. 選取報表類型。

    您可以選擇下列其中一種或兩種報表類型:
    * 檢查資料庫相容性
    * 檢查功能同位

   ![Azure Migrate-Data Migration Assistant-評量選項畫面](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-options-screen.png)

2. 選取 [下一步]。

### <a name="add-databases-to-assess"></a>新增要評估的資料庫

1. 選取 [**新增來源**] 以開啟 [連線飛出] 功能表。
2. 輸入 SQL server 實例名稱、選擇 [驗證類型]、設定正確的 [連接屬性], 然後選取 **[連線]** 。
3. 選取要評估的資料庫, 然後選取 [**新增**]。

   > [!NOTE]
   > 您可以選取多個資料庫, 同時按住 Shift 或 Ctrl 鍵, 然後按一下 [移除來源]。 您也可以使用 [新增來源] 按鈕, 從多個 SQL Server 實例新增資料庫。

4. 選取 **[下一步]** 以開始評量。

   ![Azure Migrate-Data Migration Assistant-選取來源畫面](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-select-sources-screen.png)

5. 評估完成後, 選取 **[上傳至 Azure Migrate**]。

   ![Azure Migrate-Data Migration Assistant-審查結果畫面](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-review-results-screen.png)

6. 登入 Azure 入口網站。

   ![Azure Migrate-Data Migration Assistant-審查結果畫面](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-portal-signin.png)

7. 選取您要上傳評估結果的訂用帳戶和 Azure Migrate 專案, 然後選取 [**上傳**]。

   等待評估上傳確認。

## <a name="view-target-readiness-assessment-results"></a>查看目標就緒評估結果

1. 登入 Azure 入口網站, 搜尋 [Azure 遷移], 然後選取 [ **Azure Migrate**]。

   ![Azure Migrate-Azure 入口網站-服務搜尋](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-portal-search.png)

2. 選取 [**評估並遷移資料庫**] 以取得評量結果。

   ![Azure Migrate 審查評估結果](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-hub-assess.png)

    您可以查看 SQL Server 的準備就緒摘要, 確定您是在正確的遷移專案上, 否則請使用 [變更] 選項來選取不同的遷移專案。

    每次您將評估結果更新為 Azure 遷移專案時, Azure 遷移中樞會合並所有結果並提供摘要報告。  您可以平行執行數個 Data Migration Assistant 評量, 並將結果上傳至單一的「遷移」專案, 以取得匯總的準備報告。

   ![Azure Migrate-審查準備就緒結果](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-review-readiness.png)

    已**評估的資料庫實例**:目前為止已評估的 SQL Server 實例數目。
    已**評估的資料庫**:已評估一或多個 SQL Server 實例的資料庫總數評估已**準備好用於 SQL DB 的資料庫**:準備要遷移至 Azure SQL Database (PaaS) 的資料庫數目。
    **準備好用於 AZURE SQL VM 的資料庫**:資料庫數目會包含一或多個遷移封鎖器至 Azure SQL Database (PaaS), 但可供遷移至 Azure SQL Server Vm。

3. 選取 [已**評估的資料庫實例**], 以取得 SQL Server 實例層級的視圖。

   ![Azure Migrate 審核實例就緒](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-assessed-instances.png)

    您可以找出遷移至 Azure SQL Database (PaaS) 之每個 SQL Server 實例的準備就緒狀態百分比。

4. 選取特定實例, 以取得資料庫就緒性視圖。

   ![Azure Migrate-審查資料庫的就緒程度](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-assessed-databases.png)

    您可以查看每個資料庫的遷移封鎖器數目, 這是上述視圖中每個資料庫的建議目標。

5. 請參閱 DMA 評估結果, 以取得更多有關遷移封鎖器的詳細資料。

   ![Azure Migrate-審查遷移封鎖器](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-migration-blockers.png)

## <a name="see-also"></a>另請參閱

* [Data Migration Assistant (DMA)](../dma/dma-overview.md)
* [Data Migration Assistant:設定](../dma/dma-configurationsettings.md)
* [Data Migration Assistant:最佳做法](../dma/dma-bestpractices.md)
