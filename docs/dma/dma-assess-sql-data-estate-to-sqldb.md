---
title: 評估 SQL Server 準備好遷移至 Azure SQL Database
titleSuffix: Data Migration Assistant
description: 瞭解如何使用 Data Migration Assistant 將 SQL Server 資料資產遷移至 Azure SQL Database
ms.date: 12/19/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, on-premises SQL Server
ms.assetid: ''
author: rajeshsetlem
ms.author: rajpo
ms.custom: seo-lt-2019
ms.openlocfilehash: 9aae42b92c6d7d9bb5c26c84e49c49a8cde6bc57
ms.sourcegitcommit: 67befbf7435f256e766bbce6c1de57799e1db9ad
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/24/2020
ms.locfileid: "92523875"
---
# <a name="assess-the-readiness-of-a-sql-server-data-estate-migrating-to-azure-sql-database-using-the-data-migration-assistant"></a>使用 Data Migration Assistant 來評估 SQL Server 資料資產遷移至 Azure SQL Database 的就緒程度

將數百個 SQL Server 實例和數千個資料庫移轉至 Azure SQL Database，我們的平臺即服務 (PaaS) 供應專案，是相當重要的工作。 若要盡可能簡化此程式，您必須安心地瞭解遷移的相對就緒程度。 找出低度的水果（包括已完全就緒或需要最少努力的伺服器和資料庫，以準備進行遷移），簡化並加速您的工作。

本文提供逐步指示，說明如何利用 [Data Migration Assistant](./dma-overview.md?view=sql-server-2017) 摘要就緒結果，並在 [Azure Migrate](https://portal.azure.com/?feature.customPortal=false#blade/Microsoft_Azure_Migrate/AmhResourceMenuBlade/overview) 中樞呈現這些結果。

>
> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Data-Migration-Assistant/player?WT.mc_id=dataexposed-c9-niner]

## <a name="create-a-project-and-add-a-tool"></a>建立專案並新增工具

在 Azure 訂用帳戶中設定新的 Azure Migrate 專案，然後新增工具。

Azure Migrate 專案可用來儲存從您評估或遷移的環境中收集到的探索、評量和移轉中繼資料。 您也可以使用專案來追蹤探索到的資產，以及協調評定和遷移。

1. 登入 Azure 入口網站，選取 [ **所有服務**]，然後搜尋 Azure Migrate。
2. 在 [服務] 下，選取 [Azure Migrate]。

   ![Azure Migrate-選取服務](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-services.png)

3. 在 [ **總覽** ] 頁面上，選取 [ **評估和遷移資料庫**]。

   ![Azure Migrate-起始評量](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-hub-assess.png)

4. 在 [ **資料庫**] 的 **[開始使用] 底下，選取**[ **新增工具 (s]) **。

   ![Azure Migrate-新增工具](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-add-tools.png)

5. 在 [ **遷移專案** ] 索引標籤上，選取您的 Azure 訂用帳戶和資源群組 (如果您還沒有資源群組，請建立一個) 。
6. 在 [ **專案詳細資料**] 底下，指定專案名稱以及要在其中建立專案的地理位置。

    ![Azure Migrate-新增工具對話方塊](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-add-tool-dialog.png)

    您可以在下列任何地理位置建立 Azure Migrate 專案。

    | **地理位置**  | **儲存體位置區域** |
    | ------------- | ------------- |
    | Asia | 東南亞或東亞 |
    | 歐洲 | 歐洲南部或西歐 |
    | United Kingdom | 英國南部或英國西部 |
    | 美國 | 美國中部或美國西部 2 |

    針對專案所指定的地理位置，僅會用於儲存從內部部署虛擬機器收集的中繼資料。 您可以選取任何目標區域以進行實際移轉。

7. 選取 **[下一步]**，然後新增評量工具。

   > [!NOTE]
   > 當您建立專案時，您必須新增至少一個評量或遷移工具。

8. 在 [ **選取評估工具** ] 索引標籤上， **Azure Migrate：資料庫評** 量會顯示為要新增的評量工具。 如果您目前不需要評量工具，請選取 [ **立即略過新增評估工具** ] 核取方塊。 選取 [下一步]  。

    ![Azure Migrate-選取評量工具索引標籤](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-select-assessment-tool.png)

9. 在 [ **選取遷移工具** ] 索引標籤上， **Azure Migrate：資料庫移轉** 會顯示為要加入的遷移工具。 如果您目前不需要遷移工具，請選取 [ **立即略過新增遷移工具**]。 選取 [下一步]  。

    ![Azure Migrate-選取遷移工具索引標籤](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-select-migration-tool.png)

10. 在 [ **檢查 + 新增工具**] 中，檢查設定，然後選取 [ **新增工具**]。

    ![Azure Migrate-評論 + 新增工具 (s) 索引標籤](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-review-tools.png)

    建立專案之後，您可以選取其他工具來評估和遷移伺服器和工作負載、資料庫和 web 應用程式。

## <a name="assess-and-upload-assessment-results"></a>評估及上傳評量結果

在您成功建立遷移專案之後，請在 [ **評量工具**] 的 [ **Azure Migrate：資料庫評估** ] 方塊中，下載並使用 Data Migration Assistant 工具顯示的指示。

   ![已新增 Azure Migrate 評定工具](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-assessment-tool-added.png)

1. 使用提供的連結下載 Data Migration Assistant，然後將它安裝在可存取來源 SQL Server 實例的電腦上。
2. 啟動 [Data Migration Assistant]。

### <a name="create-an-assessment"></a>建立評估

1. 選取左側的 **+** 圖示，然後選取 [評定] **專案類型**
2. 指定專案名稱，然後選取來源伺服器和目標伺服器類型。

    如果您要將內部部署 SQL Server 實例升級至較新版本的 SQL Server 或 SQL Server 裝載于 Azure VM 上，請將來源和目標伺服器類型設定為 **SQL Server**。 將 [目標伺服器類型] 設定為 [ **AZURE SQL 受控執行個體** ]，Azure SQL Database (PaaS) 目標準備評估。

3. 選取 [建立]。

   ![Azure Migrate Data Migration Assistant 介面](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-interface.png)

### <a name="choose-assessment-options"></a>選擇評量選項

1. 選取報表類型。

    您可以選擇下列其中一種或兩種報表類型：
    * 檢查資料庫相容性
    * 檢查功能同位

   ![Azure Migrate-Data Migration Assistant-評量選項畫面](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-options-screen.png)

2. 選取 [下一步]  。

### <a name="add-databases-to-assess"></a>新增要評估的資料庫

1. 選取 [ **新增來源** ] 以開啟 [連接飛出] 功能表。
2. 輸入 SQL server 實例名稱，選擇驗證類型，設定正確的連接屬性，然後選取 **[連接]**。
3. 選取要評估的資料庫，然後選取 [ **新增**]。

   > [!NOTE]
   > 您可以選取多個資料庫，同時按住 Shift 或 Ctrl 鍵，然後按一下 [移除來源]，以移除多個資料庫。 您也可以使用 [加入來源] 按鈕，從多個 SQL Server 實例加入資料庫。

4. 選取 [下一步] 開始進行評估。

   ![Azure Migrate-Data Migration Assistant-選取來源畫面](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-select-sources-screen.png)

5. 評量完成後，請選取 **[上傳至 Azure Migrate**]。

   ![螢幕擷取畫面，顯示已呼叫 [上傳至 Azure Migrate] 選項的 Data Migration Assistant。](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-review-results-screen.png)

6. 登入 Azure 入口網站。

   ![顯示 Azure 入口網站登入視窗之 Data Migration Assistant 的螢幕擷取畫面。](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-portal-signin.png)

7. 選取您要上傳評量結果的訂用帳戶和 Azure Migrate 專案，然後選取 [ **上傳**]。

   等候評定上傳確認。

## <a name="view-target-readiness-assessment-results"></a>查看目標就緒程度評定結果

1. 登入 Azure 入口網站、搜尋 Azure 遷移，然後選取 [ **Azure Migrate**]。

   ![Azure Migrate-Azure 入口網站-服務搜尋](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-portal-search.png)

2. 選取 [ **評估和遷移資料庫** ] 以取得評量結果。

   ![Azure Migrate-審核評定結果](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-hub-assess.png)

    您可以查看 SQL Server 就緒摘要，確定您是在正確的遷移專案上，否則請使用 [變更] 選項來選取不同的遷移專案。

    每次您將評量結果更新為 Azure 遷移專案時，Azure 遷移中樞會合並所有結果並提供摘要報告。  您可以平行執行數個 Data Migration Assistant 評量，並將結果上傳至單一遷移專案，以取得合併的就緒報告。

   ![Azure Migrate 審核準備結果](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-review-readiness.png)

    **評估的資料庫實例**：到目前為止評定的 SQL Server 實例數目。
    **評估的資料庫**：在一或多個 SQL Server 實例評估的資料庫中評估的資料庫總數 **，可供 SQL Database**：準備遷移至 Azure SQL Database (PaaS) 的資料庫數目。
    **適用于 AZURE SQL VM 的資料庫**：資料庫數目包含一或多個遷移封鎖器，可 Azure SQL Database (PaaS) ，但已準備好遷移至 Azure SQL Server vm。

3. 選取 **評估的資料庫實例** ，以取得 SQL Server 實例層級的觀點。

   ![Azure Migrate 審核實例就緒程度](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-assessed-instances.png)

    您可以找到遷移至 Azure SQL Database (PaaS) 的每個 SQL Server 實例的準備就緒狀態百分比。

4. 選取特定的實例，以取得資料庫就緒狀態。

   ![Azure Migrate 審核資料庫就緒程度](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-assessed-databases.png)

    您可以看到每個資料庫的遷移封鎖器數目，在上述的每個資料庫中，建議的目標。

5. 請參閱 DMA 評估結果，以取得更多有關遷移封鎖器的詳細資料。

   ![Azure Migrate-審核遷移封鎖器](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-migration-blockers.png)

## <a name="see-also"></a>另請參閱

* [Data Migration Assistant (DMA)](../dma/dma-overview.md) \(英文\)
* [Data Migration Assistant： Configuration settings](../dma/dma-configurationsettings.md)
* [Data Migration Assistant：最佳作法](../dma/dma-bestpractices.md)