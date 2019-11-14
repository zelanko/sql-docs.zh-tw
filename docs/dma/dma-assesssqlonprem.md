---
title: 執行 SQL Server 遷移評估
titleSuffix: Data Migration Assistant
description: 瞭解如何使用 Data Migration Assistant 來評估內部部署 SQL Server，然後再遷移至另一個 SQL Server 或 Azure SQL Database
ms.custom: seo-lt-2019
ms.date: 08/08/2019
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
ms.openlocfilehash: b2ec2f0f7030db2928a2a1e1c4f39ec62ed830ad
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056627"
---
# <a name="perform-a-sql-server-migration-assessment-with-data-migration-assistant"></a>使用 Data Migration Assistant 執行 SQL Server 遷移評估

下列逐步指示可協助您執行第一次評估，以遷移至內部部署 SQL Server、SQL Server 在 Azure VM 上執行，或使用 Data Migration Assistant 來 Azure SQL Database。

## <a name="create-an-assessment"></a>建立評量

1. 選取 [**新增**] （+）圖示，然後選取 [**評估**] 專案類型。

2. 設定來源和目標伺服器類型。

    如果您要將內部部署 SQL Server 實例升級至現代化內部部署 SQL Server 實例，或將 Azure VM 上裝載的 SQL Server，請將來源和目標伺服器類型設定為 [ **SQL Server**]。 如果您要遷移至 Azure SQL Database，請改為將目標伺服器類型設定為 [ **Azure SQL Database**]。

3. 按一下 **[建立]** 。

   ![建立評量](../dma/media/dma-assesssqlonprem/new-assessment.png)

## <a name="choose-assessment-options"></a>選擇評量選項

1. 選取您打算遷移的目標 SQL Server 版本。

2. 選取報表類型。

   當您評估來源 SQL Server 實例以遷移至內部部署 SQL Server 或裝載于 Azure VM 目標上的 SQL Server 時，您可以選擇下列其中一種或兩種評估報告類型：

    - **相容性問題**
    - **新功能的建議**

   ![選取 SQL Server 目標的評量報告類型](../dma/media/dma-assesssqlonprem/assessment-types.png)

   評估來源 SQL Server 實例以遷移至 Azure SQL Database 時，您可以選擇下列其中一種或兩種評估報告類型：

    - **檢查資料庫相容性**
    - **檢查功能同位**

    ![選取 SQL Database 目標的評量報告類型](../dma/media/dma-assesssqlonprem/assessment-types-azure.png)

## <a name="add-databases-and-extended-events-trace-to-assess"></a>新增資料庫和擴充事件追蹤以進行評估

1. 選取 [**新增來源**] 以開啟 [連線] 飛出視窗功能表。

2. 輸入 SQL server 實例名稱、選擇 [驗證類型]、設定正確的 [連接屬性]，然後選取 **[連線]** 。

3. 選取要評估的資料庫，然後選取 [**新增**]。

    > [!NOTE]
    > 您可以選取多個資料庫，同時按住 Shift 或 Ctrl 鍵，然後按一下 [**移除來源**]。 您也可以選取 [**新增來源**]，從多個 SQL Server 實例新增資料庫。

4. 如果您有任何臨機操作或動態 SQL 查詢，或是透過應用程式資料層起始的任何 DML 語句，則請輸入您放置的所有擴充事件會話檔案所在的資料夾路徑，以便在來源上捕獲工作負載 SQL Server.

     下列範例顯示如何在來源 SQL Server 上建立擴充事件會話，以捕捉應用程式資料層工作負載。  在代表尖峰工作負載的持續時間內，捕獲工作負載。

    ```
    DROP EVENT SESSION [DatalayerSession] ON SERVER
    go
    CREATE EVENT SESSION [DatalayerSession] ON SERVER  
    ADD EVENT sqlserver.sql_statement_completed( 
        ACTION (sqlserver.sql_text,sqlserver.client_app_name,sqlserver.client_hostname,sqlserver.database_id))
    ADD TARGET package0.asynchronous_file_target(SET filename=N'C:\temp\Demos\DataLayerAppassess\DatalayerSession.xel')  
    WITH (MAX_MEMORY=2048 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=3 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=OFF)
    go
    ---Start the session
    ALTER EVENT SESSION [DatalayerSession]
          ON SERVER
        STATE = START;
    ---Wait for few minutes
    
    ---Query events
        
        SELECT 
        object_name,
        CAST(event_data as xml) as event_data,
        file_name, 
        file_offset
    FROM sys.fn_xe_file_target_read_file('C:\temp\Demos\DataLayerAppassess\DatalayerSession*xel', 
                'C:\\temp\\Demos\\DataLayerAppassess\\DatalayerSession*xem', 
                null,
                null)
    ---Stop the session after capturing the peak load.
    ALTER EVENT SESSION [DatalayerSession]
          ON SERVER
        STATE = STOP;
        
        go
    ```

5. 按 **[下一步]** 開始進行評量。

    ![新增來源並開始評估](../dma/media/dma-assesssqlonprem/select-database1.png)

## <a name="view-results"></a>檢視結果

評量的持續時間取決於新增的資料庫數目和每個資料庫的架構大小。 每個資料庫一旦出現就會顯示結果。

1. 選取已完成評估的資料庫，然後使用切換器切換**相容性問題**和**功能建議**。

2. 檢查您在 [**選項**] 頁面上選取的目標 SQL Server 版本所支援之所有相容性層級的相容性問題。

您可以分析受影響的物件、其詳細資料，並可能修正**重大變更**、**行為變更**和已**淘汰功能**所識別的每個問題，以檢查相容性問題。

![查看評估結果](../dma/media/dma-assesssqlonprem/review-results.png)

同樣地，您可以在**效能**、**儲存體**和**安全性**區域中查看功能建議。

功能建議涵蓋不同種類的功能，例如記憶體內部 OLTP、資料行存放區、Stretch Database、Always Encrypted、動態資料遮罩和透明資料加密。

![View 功能建議](../dma/media/dma-assesssqlonprem/feature-recommendations.png)

針對 Azure SQL Database，評量會提供遷移封鎖問題和功能同位問題。 選取特定的選項，以檢查這兩個類別的結果。

- **SQL Server 功能**同位類別提供一組完整的建議、Azure 中可用的替代方法，以及緩和步驟。 這可協助您在遷移專案中規劃這項工作。

  ![SQL Server 功能同位的視圖資訊](../dma/media/dma-assesssqlonprem/sql-feature-parity.png)

- [**相容性問題**] 類別提供部分支援或不支援的功能，以封鎖將內部部署 SQL Server 資料庫移轉至 Azure SQL 資料庫。 接著，它會提供可協助您解決這些問題的建議。

  ![查看相容性問題](../dma/media/dma-assesssqlonprem/compatibility-issues.png)

## <a name="assess-a-data-estate-for-target-readiness"></a>評估資料資產的目標就緒程度

如果您想要進一步將這些評量延伸至整個資料資產，並找出 SQL Server 實例和資料庫的相對就緒，以便遷移至 Azure SQL Database，請選取 [**上傳至 Azure Migrate**]，將結果上傳至 Azure 遷移中樞。

這麼做可讓您在 Azure 遷移中樞專案上查看合併的結果。

如需目標就緒評量的詳細逐步指引，請參閱[這裡](https://docs.microsoft.com/sql/dma/dma-assess-sql-data-estate-to-sqldb?view=sql-server-2017)。

   ![將結果上傳至 Azure Migrate](../dma/media/dma-assesssqlonprem/upload-to-azure-migrate.png)

## <a name="export-results"></a>匯出結果

在所有資料庫完成評估之後，請選取 [**匯出報表**]，將結果匯出至 JSON 檔案或 CSV 檔案。 然後您就可以方便地分析資料。

您可以同時執行多個評量，並藉由開啟 [**所有評估**] 頁面來查看評估的狀態。
