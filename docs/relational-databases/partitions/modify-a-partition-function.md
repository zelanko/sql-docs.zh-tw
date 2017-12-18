---
title: "修改資料分割函式 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: partitions
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-partition
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ae5bfc09-f27a-4ea9-9518-485278b11674
caps.latest.revision: "11"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: e6951b2a5363c78238c38956fa90d0cfd107f919
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="modify-a-partition-function"></a>修改資料分割函數
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 您可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] ，在資料分割資料表或索引的資料分割函數中，加上或減去指定的資料分割數 (遞增為 1)，藉以變更 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中資料表或索引的資料分割方式。 若要加入資料分割，可以將現有資料分割「拆解」為兩個資料分割，並重新定義新資料分割的界限。 若要卸除資料分割，可以將兩個資料分割的界限「合併」成為一個。 最後這個動作會重新擴展一個資料分割，並使另一個資料分割成為未指派。  
  
> [!CAUTION]  
>  多份資料表或索引可以使用相同的資料分割函數。 當您修改資料分割函數時，將會在單一交易中影響所有資料表或索引。 修改之前，請先檢查資料分割函數的相依性。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要使用下列項目來修改資料分割函數：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   ALTER PARTITION FUNCTION 只能用來將一個資料分割拆解成兩個，或將兩個資料分割合併為一個。 若要變更資料表或索引的資料分割方式 (例如，從 10 個資料分割變更成 5 個)，您可以使用下列任何一個選項：  
  
    -   使用所需的資料分割函數來建立新的資料分割資料表，然後再使用 INSERT INTO ...SELECT FROM [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的 [管理資料分割精靈]，將舊資料表中的資料插入新資料表中。  
  
    -   建立堆積的資料分割叢集索引。  
  
        > [!NOTE]  
        >  卸除資料分割叢集索引會產生資料分割堆積。  
  
    -   利用設定了 DROP EXISTING = ON 子句的 [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE INDEX 陳述式來卸除和重建現有的資料分割索引。  
  
    -   執行 ALTER PARTITION FUNCTION 陳述式的序列。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不提供修改資料分割函數的複寫支援。 如果您要變更發行集資料庫中的資料分割函數，必須在訂閱資料庫中手動執行此作業。  
  
-   ALTER PARITITION FUNCTION 所影響的所有檔案群組都必須在線上。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 下列中的任何權限都可用來執行 ALTER PARTITION FUNCTION：  
  
-   ALTER ANY DATASPACE 權限。 這個權限預設會授與 **sysadmin** 固定伺服器角色以及 **db_owner** 和 **db_ddladmin** 固定資料庫角色的成員。  
  
-   對於建立資料分割函數之資料庫的 CONTROL 或 ALTER 權限。  
  
-   對於建立資料分割函數之資料庫伺服器的 CONTROL SERVER 或 ALTER ANY DATABASE 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **若要修改資料分割函數：**  
  
 您無法使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]來執行這項特定動作。 若要修改資料分割函數，您必須先刪除此函數，然後再使用 [建立資料分割精靈] 來建立具有所需屬性的新函數。 如需詳細資訊，請參閱  
  
#### <a name="to-delete-a-partition-function"></a>若要刪除資料分割函數  
  
1.  展開您想要刪除資料分割函數的資料庫，然後展開 **[儲存體]** 資料夾。  
  
2.  展開 **[資料分割函數]** 資料夾。  
  
3.  以滑鼠右鍵按一下您想要刪除的資料分割函數，然後選取 [刪除]。  
  
4.  在 **[刪除物件]** 對話方塊中，確定已選取正確的資料分割函數，然後按一下 **[確定]**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-split-a-single-partition-into-two-partitions"></a>若要將單一資料分割拆解成兩個資料分割  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    -- Look for a previous version of the partition function “myRangePF1” and deletes it if it is found.  
    IF EXISTS (SELECT * FROM sys.partition_functions  
        WHERE name = 'myRangePF1')  
        DROP PARTITION FUNCTION myRangePF1;  
    GO  
    -- Create a new partition function called “myRangePF1” that partitions a table into four partitions.  
    CREATE PARTITION FUNCTION myRangePF1 (int)  
    AS RANGE LEFT FOR VALUES ( 1, 100, 1000 );  
    GO  
    --Split the partition between boundary_values 100 and 1000  
    --to create two partitions between boundary_values 100 and 500  
    --and between boundary_values 500 and 1000.  
    ALTER PARTITION FUNCTION myRangePF1 ()  
    SPLIT RANGE (500);  
    ```  
  
#### <a name="to-merge-two-partitions-into-one-partition"></a>若要將兩個資料分割合併成一個資料分割  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    -- Look for a previous version of the partition function “myRangePF1” and deletes it if it is found.  
    IF EXISTS (SELECT * FROM sys.partition_functions  
        WHERE name = 'myRangePF1')  
        DROP PARTITION FUNCTION myRangePF1;  
    GO  
    -- Create a new partition function called “myRangePF1” that partitions a table into four partitions.  
    CREATE PARTITION FUNCTION myRangePF1 (int)  
    AS RANGE LEFT FOR VALUES ( 1, 100, 1000 );  
    GO  
    --Merge the partitions between boundary_values 1 and 100  
    --and between boundary_values 100 and 1000 to create one partition  
    --between boundary_values 1 and 1000.  
    ALTER PARTITION FUNCTION myRangePF1 ()  
    MERGE RANGE (100);  
    ```  
  
 如需詳細資訊，請參閱 [ALTER PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-partition-function-transact-sql.md)。  
  
  
