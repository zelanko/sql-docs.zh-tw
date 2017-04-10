---
title: "PolyBase 向外延展群組 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "05/24/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine-polybase"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "PolyBase"
  - "PolyBase, 向外延展群組"
  - "向外延展 PolyBase"
ms.assetid: c7810135-4d63-4161-93ab-0e75e9d10ab5
caps.latest.revision: 20
author: "barbkess"
ms.author: "barbkess"
manager: "jhubbard"
caps.handback.revision: 19
---
# PolyBase 向外延展群組
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  含有 PolyBase 的獨立 SQL Server 執行個體會在處理 Hadoop 或 Azure Blob 儲存體中的大量資料集時成為效能瓶頸。 PolyBase 群組功能可讓您建立 SQL Server 執行個體的叢集，利用向外延展方式處理來自外部資料來源 (例如 Hadoop 或 Azure Blob 儲存體) 的大型資料集，以提高查詢效能。  
  
 請參閱[開始使用 PolyBase](../../relational-databases/polybase/get-started-with-polybase.md) 和 [PolyBase 指南](../../relational-databases/polybase/polybase-guide.md)。  
  
 ![PolyBase scale-out groups](../../relational-databases/polybase/media/polybase-scale-out-groups.png "PolyBase scale-out groups")  
  
## 概觀  
  
### 前端節點  
 前端節點包含要提交 PolyBase 查詢的目標 SQL Server 執行個體。 每個 PolyBase 群組只能包含一個前端節點。 前端節點是 SQL Server 執行個體上 SQL Database Engine、PolyBase Engine 及 PolyBase Data Movement Service 的邏輯群組。  
  
### 計算節點  
 計算節點包含 SQL Server 執行個體，可協助處理外部資料上的向外延展查詢。 計算節點是 SQL Server 執行個體上 SQL Server 和 PolyBase Data Movement Service 的邏輯群組。 一個 PolyBase 群組可以有多個計算節點。  
  
### 分散式查詢處理  
 PolyBase 查詢會提交到前端節點上的 SQL Server。 參考外部資料表之查詢的這一部分會交付至 PolyBase Engine。  
  
 PolyBase Engine 是 PolyBase 查詢背後的重要元件。 它會剖析外部資料的查詢、產生查詢計劃，以及將工作分散到計算節點上的資料移動服務加以執行。 工作完成之後，它會接收來自計算節點的結果，然後提交給 SQL Server 進行處理並傳回給用戶端。  
  
 PolyBase Data Movement Service 會接收來自 PolyBase Engine 的指示，並在 HDFS 與 SQL Server 之間傳輸資料，以及在前端和計算節點上的 SQL Server 執行個體之間傳輸資料。  
  
### 版本可用性  
 安裝 SQL Server 之後，可以指定執行個體做為前端節點或計算節點。  這個選擇取決於 PolyBase 執行所在的是哪一個 SQL Server 版本。 在 Enterprise Edition 安裝中，可以指定執行個體做為前端節點或計算節點。 在 Standard Edition 中，只能將執行個體指定為計算節點。  
  
## 設定 PolyBase 群組  
  
### 必要條件  
  
-   位於相同網域的 N 部電腦  
  
-   一個執行 PolyBase 服務的網域使用者帳戶  
  
### 步驟  
  
1.  在 N 部電腦上安裝含有 PolyBase 的 SQL Server。  
  
2.  選取一個 SQL Server 執行個體做為前端節點。 只可在執行 SQL Server Enterprise 的執行個體中指定前端節點。  
  
3.  使用 [sp_polybase_join_group](../Topic/sp_polybase_join_group.md)，加入其餘的 SQL Server 執行個體作為計算節點。  
  
4.  使用 [sys.dm_exec_compute_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md) 監視群組中的節點。  
  
5.  選擇性。 使用 [sp_polybase_leave_group &#40;Transact-SQL&#41;](../Topic/sp_polybase_leave_group%20\(Transact-SQL\).md) 移除運算節點。  
  
## 範例逐步解說  
 這會使用下列項目逐步設定 PolyBase 群組︰  
  
1.  位於網域 *PQTH4A* 中的兩部電腦 電腦名稱為︰  
  
    -   PQTH4A-CMP01  
  
    -   PQTH4A-CMP02  
  
2.  網域帳戶︰*PQTH4A\PolybaseUse*r  
  
#### 步驟 1：在所有電腦上安裝含有 PolyBase 的 SQL Server  
  
1.  執行 setup.exe。  
  
2.  在 [特徵選取] 頁面上，選取 [外部資料的 PolyBase 查詢服務] 。  
  
3.  在 [伺服器組態] 頁面上，SQL Server PolyBase 引擎和 SQL Server PolyBase 資料移動服務請使用**網域帳戶** PQTH4A\PolybaseUser。  
  
4.  在 [PolyBase 組態] 頁面上，選取 [Use the SQL Server instance as part of a PolyBase scale-out group (使用此 SQL Server 執行個體作為 PolyBase 向外延展群組的一部分)]。 這會開啟防火牆，以允許 PolyBase 服務的連入連線。  
  
5.  安裝程式完成之後，執行 **services.msc**。 確認 SQL Server、PolyBase Engine 和 PolyBase Data Movement Service 正在執行中。  
  
     ![PolyBase services](../../relational-databases/polybase/media/polybase-services.png "PolyBase services")  
  
#### 步驟 2︰選取一個 SQL Server 做為前端節點  
  
-   安裝程式完成之後，這兩部電腦可用來做為 PolyBase 群組前端節點。 在此範例中，我們將選擇 PQTH4A-CMP01 上的 "MSSQLSERVER" 做為前端節點。  
  
#### 步驟 3：加入其餘的 SQL Server 執行個體做為計算節點  
  
1.  連接到 PQTH4A-CMP02 上的 SQL Server。  
  
2.  執行預存程序 [sp_polybase_join_group](../Topic/sp_polybase_join_group.md)。  
  
    ```  
    -- Enter head node details:   
    -- head node machine name, head node dms control channel port, head node sql server name  
    EXEC sp_polybase_join_group 'PQTH4A-CMP01', 16450, 'MSSQLSERVER';  
  
    ```  
  
3.  在計算節點 (PQTH4A-CMP02) 上執行 services.msc。  
  
4.  關閉 PolyBase Engine 並重新啟動 PolyBase Data Movement Service。  
  
#### 選擇性：移除計算節點  
  
1.  連接到計算節點 SQL Server (PQTH4A-CMP02)。  
  
2.  執行預存程序 sp_polybase_leave_group。  
  
    ```  
    EXEC sp_polybase_leave_group;  
    ```  
  
3.  在已移除的計算節點 (PQTH4A-CMP02) 上執行 services.msc。  
  
4.  啟動 PolyBase Engine。 重新啟動 PolyBase Data Movement Service。  
  
5.  在 PQTH4A-CMP01 上執行 DMV sys.dm_exec_compute_nodes，確認節點已移除。 現在，PQTH4A-CMP02 將可用來做為獨立的前端節點  
  
## 後續的步驟  
 如需疑難排解，請參閱 [PolyBase troubleshooting with dynamic management views](../Topic/PolyBase%20troubleshooting%20with%20dynamic%20management%20views.md)。  
  
## 另請參閱  
 [開始使用 PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)   
 [PolyBase 指南](../../relational-databases/polybase/polybase-guide.md)   
 [PolyBase 連線組態 &#40;Transact-SQL&#41;](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)  
  
  