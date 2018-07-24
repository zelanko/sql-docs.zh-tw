---
title: 指定索引的填滿因素 | Microsoft Docs
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- fill factor [SQL Server]
- page splits [SQL Server]
ms.assetid: 237a577e-b42b-4adb-90cf-aa7fb174f3ab
caps.latest.revision: 45
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 251c250306d01eb14cdde76ce09cfd9b81fdf203
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38054518"
---
# <a name="specify-fill-factor-for-an-index"></a>指定索引的填滿因素
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  此主題描述何謂填滿因數，以及如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中指定索引的填滿因數值。  
  
 提供填滿因數的用意，是為了微調索引資料的儲存與效能。 建立或重建索引時，填滿因數值會決定要在每個分葉層級頁面上填滿資料的空間百分比，進而保留每個頁面的剩餘百分比當做可用空間，以供未來成長使用。 例如，如果指定填滿因數值 80，則表示每個分葉層級的頁面將有百分之 20 的空間保留空白，在基礎資料表中加入資料時，將有空間可供索引擴充使用。 索引資料列之間 (而不是索引結尾處) 的空白空間將會予以保留。  
  
 填滿因數值是 1 到 100 之間的百分比，而整個伺服器的預設值 0 則表示分葉層級頁面的容量填滿。  
  
> [!NOTE]  
>  填滿因數值 0 和 100 在各方面都是一樣的。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [效能考量](#Performance)  
  
     [Security](#Security)  
  
-   **使用下列方法指定索引的填滿因數：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Performance"></a> 效能考量  
  
#### <a name="page-splits"></a>頁面分割  
 選擇正確的填滿因數值，可以減少可能的頁面分割，因為當基礎資料表中加入資料時，將有足夠的空間來進行索引擴充。將新的資料列加入全文檢索頁面時， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會將幾乎一半的資料列移到新的頁面，以留出空間給新的資料列。 這個重組動作稱為分頁分割。 分頁分割可留出空間給新的記錄，但是執行時需要時間，而且是一項耗用大量資源的作業。 此外，它也可能會造成資料片段過多，因而增加 I/O 作業。 如果頁面分割次數過於頻繁，可以使用新的或現有的填滿因數值重建索引，藉以重新分配資料。 如需詳細資訊，請參閱 [重新組織與重建索引](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)。  
  
 雖然非零的較低填滿函數值能夠減少索引成長時進行頁面分割的需求，但是索引將需要更多的儲存空間，而且可能會降低讀取效能。 即使對於會大量執行插入和更新作業的應用程式而言，讀取資料庫的次數通常比寫入資料庫的次數還要高，因數為 5 比 10。 因此，指定預設值以外的填滿因數，將可能以與填滿因數設定呈反比的數量，降低資料庫的讀取效能。 例如，一個 50 的填滿因數值，可能會使資料庫的讀取效能降低兩倍。 讀取效能降低是因為索引包含更多的分頁，造成擷取資料所需的磁碟 IO 作業增加所致。  
  
#### <a name="adding-data-to-the-end-of-the-table"></a>將資料加入資料表的結尾  
 如果新的資料在資料表內平均分配，則非零的填滿因數值 (0 或 100 以外) 對於效能將很有幫助。 但是，如果將所有資料加入資料表的結尾，索引頁面中的空白處將不會填滿。 例如，如果索引鍵資料行為 IDENTITY 資料行，新資料列的索引鍵一定會增加，而且在邏輯上會將索引資料列加入索引的結尾。 如果現有的資料列將以增加資料列大小的資料進行更新，請使用小於 100 的填滿因數。 每個頁面上的額外位元組將有助於減少資料列中額外長度所導致的頁面分割。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 需要資料表或檢視表的 ALTER 權限。 使用者必須是 **系統管理員** 固定伺服器角色的成員，或是 **db_ddladmin** 和 **db_owner** 固定資料庫角色的成員。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-specify-a-fill-factor-by-using-table-designer"></a>使用資料表設計工具指定填滿因數  
  
1.  在 [物件總管] 中，按一下加號展開資料庫，此資料庫包含您要指定索引填滿因數的資料表。  
  
2.  按一下加號展開 **[資料表]** 資料夾。  
  
3.  以滑鼠右鍵按一下要指定索引填滿因數的資料表，然後選取 [設計]。  
  
4.  在 [資料表設計工具] 功能表上，按一下 [索引/索引鍵]。  
  
5.  選取包含您要指定填滿因數的索引。  
  
6.  展開 **[填滿規格]**，選取 **[填滿因數]** 資料列，在資料列中輸入所要的填滿因數。  
  
7.  按一下 [ **關閉**]。  
  
8.  在 [檔案] 功能表上，選取 [儲存 <資料表名稱>]。  
  
#### <a name="to-specify-a-fill-factor-in-an-index-by-using-object-explorer"></a>使用物件總管指定索引的填滿因數  
  
1.  在 [物件總管] 中，按一下加號展開資料庫，此資料庫包含您要指定索引填滿因數的資料表。  
  
2.  按一下加號展開 **[資料表]** 資料夾。  
  
3.  按一下加號展開要指定索引填滿因數的資料表。  
  
4.  按一下加號展開 **[索引]** 資料夾。  
  
5.  以滑鼠右鍵按一下包含您要指定填滿因數的索引，然後選取 [屬性]。  
  
6.  在 **[選取頁面]** 底下，選取 **[選項]**。  
  
7.  在 **[填滿因數]** 資料列中，輸入所要的填滿因數。  
  
8.  按一下 [確定] 。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-specify-a-fill-factor-in-an-existing-index"></a>若要在現有索引中指定填滿因數  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。 這個範例會重建現有的索引，並且在重建作業期間套用指定的填滿因數。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Rebuilds the IX_Employee_OrganizationLevel_OrganizationNode index   
    -- with a fill factor of 80 on the HumanResources.Employee table.  
  
    ALTER INDEX IX_Employee_OrganizationLevel_OrganizationNode ON HumanResources.Employee  
    REBUILD WITH (FILLFACTOR = 80);   
    GO  
    ```  
  
#### <a name="another-way-to-specify-a-fill-factor-in-an-index"></a>指定索引填滿因數的另一個方法  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    /* Drops and re-creates the IX_Employee_OrganizationLevel_OrganizationNode index on the HumanResources.Employee table with a fill factor of 80.  
    */  
  
    CREATE INDEX IX_Employee_OrganizationLevel_OrganizationNode ON HumanResources.Employee  
       (OrganizationLevel, OrganizationNode)   
    WITH (DROP_EXISTING = ON, FILLFACTOR = 80);   
    GO  
    ```  
  
 如需詳細資訊，請參閱 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)。  
  
  
