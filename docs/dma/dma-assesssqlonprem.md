---
title: 執行 SQL Server 移轉評估
titleSuffix: Data Migration Assistant
description: 瞭解如何在移到其他 SQL 伺服器或 Azure SQL 資料庫之前使用資料遷移助手評估本地 SQL 伺服器
ms.date: 01/15/2020
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
ms.custom: seo-lt-2019
ms.openlocfilehash: 59dc8c96ebda5ac66fb6701d480cb6d633e83158
ms.sourcegitcommit: 48e259549f65f0433031ed6087dbd5d9c0a51398
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/07/2020
ms.locfileid: "80809746"
---
# <a name="perform-a-sql-server-migration-assessment-with-data-migration-assistant"></a>使用 Data Migration Assistant 來執行 SQL Server 移轉評估

以下分步說明可説明您使用資料遷移助手執行第一次評估,以便遷移到本地 SQL 伺服器、在 Azure VM 上運行的 SQL Server 或 Azure SQL 資料庫。

   > [!NOTE]
   > 數據移轉助手 v5.0 引入了對分析應用程式代碼中的資料庫連接和嵌入式 SQL 查詢的支援。 有關詳細資訊,請參閱[博客文章"使用數據遷移助手評估應用程式的數據訪問層](https://techcommunity.microsoft.com/t5/Microsoft-Data-Migration/Using-Data-Migration-Assistant-to-assess-an-application-s-data/ba-p/990430)"。

## <a name="create-an-assessment"></a>建立評估

1. 選擇 **「新建**(+)「圖示,然後選擇 **」評估**項目類型」。。

2. 設定來源和目標伺服器類型。

    如果要將本地 SQL Server 實體升級到現代本地 SQL Server 實體或系統在 Azure VM 上的 SQL Server,請將來源伺服器和目標伺服器類型設定為**SQL Server**。 如果要移到 Azure SQL 資料庫,則改為將目標伺服器類型設定為**Azure SQL 資料庫**。

3. 按一下頁面底部的 [新增]  。

   ![建立評估](../dma/media/dma-assesssqlonprem/new-assessment.png)

## <a name="choose-assessment-options"></a>選擇評項選項

1. 選擇計劃遷移到的目標 SQL Server 版本。

2. 選擇報表類型。

   在評估來源 SQL Server 實體以移轉到本地 SQL Server 或 Azure VM 目標上託管的 SQL Server 時,可以選擇以下一種或兩種評估報告類型:

    - **相容性問題**
    - **新功能的建議**

   ![為 SQL Server 來選擇評估報告類型](../dma/media/dma-assesssqlonprem/assessment-types.png)

   在評估來源 SQL Server 實體以移轉到 Azure SQL 資料庫時,可以選擇以下一種或兩種評估報告類型:

    - **檢查資料庫相容性**
    - **檢查功能同位**

    ![為 SQL 資料庫來選擇評估報告類型](../dma/media/dma-assesssqlonprem/assessment-types-azure.png)

## <a name="add-databases-and-extended-events-trace-to-assess"></a>新增資料庫及延伸事件追蹤以評估

1. 選擇 **「新增來源**」 以開啟連接彈出視窗選單。

2. 輸入 SQL 伺服器實體名稱,選擇身份驗證類型,設定正確的連接屬性,然後選擇 **「連接**」。

3. 選擇要評估的資料庫,然後選擇 **「添加**」。

    > [!NOTE]
    > 您可以通過在按住 Shift 或 Ctrl 鍵時選擇多個資料庫,然後單擊「**刪除來源**」來刪除多個資料庫。 還可以通過選擇 **「添加源**」從多個 SQL Server 實例添加資料庫。

4. 如果您有任何臨時或動態 SQL 查詢或透過應用程式資料層啟動的任何 DML 語句,請輸入資料夾的路徑,其中放置您收集的所有擴展事件工作階段檔以捕捉來源 SQL Server 上的工作負載。

     下面的範例展示如何在源 SQL Server 上創建擴展事件工作階段以捕獲應用程式資料層工作負載。  捕獲表示峰值工作負載的工期工作負載。

    ```
    DROP EVENT SESSION [DatalayerSession] ON SERVER
    go
    CREATE EVENT SESSION [DatalayerSession] ON SERVER  
    ADD EVENT sqlserver.sql_batch_completed( 
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

5. 按 [下一步]**** 開始進行評估。

    ![新增來源並開始評估](../dma/media/dma-assesssqlonprem/select-database1.png)

> [!NOTE]
> 您可以同時執行多個評估，並開啟 [所有評估]**** 頁面來檢視這些評估的狀態。

## <a name="view-results"></a>檢視結果

評估的持續時間取決於添加的資料庫數和每個資料庫的架構大小。 每個資料庫的結果一旦可用,就會顯示出來。

1. 選擇已完成評估的資料庫,然後使用切換器在**相容性問題和****功能建議**之間切換。

2. 查看您在 **「選項**」頁上選擇的目標 SQL Server 版本支援的所有相容性級別的相容性問題。

您可以透過分析受影響的物件、其詳細資訊,以及針對 **「中斷更改**、**行為更改**」和 **「棄用功能**」下標識的每個問題進行修復來查看相容性問題。

![檢視評結果](../dma/media/dma-assesssqlonprem/review-results.png)

同樣,您可以跨**性能**、**儲存****和安全**區域查看功能建議。

功能建議涵蓋不同類型的功能,如記憶體中 OLTP、列存儲、拉伸資料庫、始終加密、動態數據遮罩和透明數據加密。

![檢視功能建議](../dma/media/dma-assesssqlonprem/feature-recommendations.png)

對於 Azure SQL 資料庫,評估提供遷移阻止問題和功能奇偶校驗問題。通過選擇特定選項查看兩個類別的結果。

- **SQL Server 功能奇偶校驗**類別提供了一組全面的建議、Azure 中可用的替代方法以及緩解步驟。 它可以説明您在遷移專案中規劃此工作。

  ![檢視 SQL Server 功能奇偶校驗的資訊](../dma/media/dma-assesssqlonprem/sql-feature-parity.png)

- **相容性問題**類別提供了部分支援或不支援的功能,這些功能阻止將本地 SQL Server 資料庫遷移到 Azure SQL 資料庫。然後,它提供建議以説明您解決這些問題。

  ![檢視相容性問題](../dma/media/dma-assesssqlonprem/compatibility-issues.png)

## <a name="assess-a-data-estate-for-target-readiness"></a>評估目標就緒性資料區

如果希望進一步將這些評估擴展到整個資料區,並查找 SQL Server 實例和資料庫的相對就緒性,以便遷移到 Azure SQL 資料庫,請透過選擇 **「上載到 Azure 遷移**」將結果上載到 Azure 遷移中心。

這樣做允許您在 Azure 遷移中心專案上查看合併結果。

[此處](https://docs.microsoft.com/sql/dma/dma-assess-sql-data-estate-to-sqldb?view=sql-server-2017)提供了目標就緒性評估的詳細、分步指南。

   ![將結果上傳到 Azure 移轉](../dma/media/dma-assesssqlonprem/upload-to-azure-migrate.png)

## <a name="export-results"></a>匯出結果

完成所有資料庫評估後,選擇 **「匯出報告**」將結果匯出到 JSON 檔或 CSV 檔。 然後,您可以自行分析數據。

## <a name="save-and-load-assessments"></a>儲存並載入評量

除了匯出評估結果外,還可以將評估詳細資訊保存到檔中並載入評估檔以供以後審閱。  有關詳細資訊,請參閱[文章"使用數據遷移助手保存和載入評估](../dma/dma-save-load-assessments.md)"。
