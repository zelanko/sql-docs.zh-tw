---
title: 停用索引和條件約束 | Microsoft Docs
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.disableindexes.f1
helpviewer_keywords:
- disabled indexes [SQL Server], index operations
- nonclustered indexes [SQL Server], disabling
- disabled indexes [SQL Server], guidelines
- clustered indexes, disabling
- constraints [SQL Server], disabling
- disabled indexes [SQL Server], viewing
- FOREIGN KEY constraints, disabling
- statistical information [SQL Server], indexes
- index disabling [SQL Server]
- indexed views [SQL Server], disabled indexes
ms.assetid: 2198f1af-fa44-47e9-92df-f4fde322ba18
caps.latest.revision: 28
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 79f521d1e3ed356b2cac3b3a870a696712ca2349
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43060301"
---
# <a name="disable-indexes-and-constraints"></a>停用索引和條件約束
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中停用索引或條件約束。 停用索引會防止使用者存取索引，而停用叢集索引則會防止存取基礎資料表資料。 索引定義會保留在中繼資料內，而索引統計資料會保留在非叢集索引上。 停用檢視上的非叢集或叢集索引，實際上會刪除索引資料。 停用資料表上的叢集索引，則會防止存取資料；這些資料仍留在資料表中，但無法用於資料操作語言 (DML) 作業，除非卸除或重建索引。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **使用下列方法停用索引：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   索引停用時，不會進行維護。  
  
-   查詢最佳化工具在建立查詢執行計畫時，不會考慮停用的索引。 此外，使用資料表提示來參考已停用索引的查詢會失敗。  
  
-   您不能建立與現有停用之索引同名的索引。  
  
-   已停用的索引可將其卸除。  
  
-   停用唯一索引時，PRIMARY KEY 或 UNIQUE 條件約束，以及從其他資料表參考索引資料行的所有 FOREIGN KEY 條件約束，也會被停用。 停用叢集索引時，基礎資料表上的所有內送和外送 FOREIGN KEY 條件約束也會停用。 當索引停用時，會在警告訊息中列出條件約束名稱。 重建索引之後，必須使用 ALTER TABLE CHECK CONSTRAINT 陳述式來手動啟用所有條件約束。  
  
-   當關聯的叢集索引停用時，非叢集索引也會自動停用。 直到啟用資料表或檢視上的叢集索引，或卸除資料表上的叢集索引時，才可以啟用非叢集索引。 除非已使用 ALTER INDEX ALL REBUILD 陳述式啟用叢集索引，否則必須以明確方式啟用非叢集索引。  
  
-   ALTER INDEX ALL REBUILD 陳述式會重建和啟用資料表上所有已停用的索引，除了檢視上的已停用索引。 檢視上的索引必須在個別的 ALTER INDEX ALL REBUILD 陳述式中啟用。  
  
-   停用資料表上的叢集索引，也會停用參考該資料表之檢視上的所有叢集和非叢集索引。 這些索引與被參考資料表上的那些索引一樣，都必須重建。  
  
-   除了用於卸除或重建叢集索引，否則無法存取已停用叢集索引的資料列。  
  
-   當資料表沒有已停用的叢集索引時，您可以在線上重建已停用的非叢集索引。 然而，如果您使用 ALTER INDEX REBUILD 或 CREATE INDEX WITH DROP_EXISTING 陳述式，則一定要以離線方式重建已停用的叢集索引。 如需線上索引作業的詳細資訊，請參閱 [線上執行索引作業](../../relational-databases/indexes/perform-index-operations-online.md)。  
  
-   在已停用叢集索引的資料表上，CREATE STATISTICS 陳述式無法成功執行。  
  
-   當已停用索引，且符合下列情況時，AUTO_CREATE_STATISTICS 資料庫選項會在資料行上建立新的統計資料：  
  
    -   AUTO_CREATE_STATISTICS 設為 ON。  
  
    -   該資料行沒有統計資料。  
  
    -   查詢最佳化期間需要統計資料。  
  
-   如果叢集索引已停用， [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) 便無法傳回基礎資料表的相關資訊；相反地，陳述式會報告該叢集索引已停用。 [DBCC INDEXDEFRAG](../../t-sql/database-console-commands/dbcc-indexdefrag-transact-sql.md) 不能用來重組已停用的索引：陳述式會失敗並出現錯誤訊息。 您可以使用 [DBCC DBREINDEX](../../t-sql/database-console-commands/dbcc-dbreindex-transact-sql.md) 來重建已停用的索引。  
  
-   建立新的叢集索引可啟用先前停用的非叢集索引。 如需詳細資訊，請參閱 [Enable Indexes and Constraints](../../relational-databases/indexes/enable-indexes-and-constraints.md)。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 若要執行 ALTER INDEX，至少需要資料表或檢視表的 ALTER 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-disable-an-index"></a>若要停用索引  
  
1.  在 [物件總管] 中，按一下加號展開資料庫，此資料庫包含您要停用索引的資料表。  
  
2.  按一下加號展開 **[資料表]** 資料夾。  
  
3.  按一下加號展開要停用索引的資料表。  
  
4.  按一下加號展開 **[索引]** 資料夾。  
  
5.  以滑鼠右鍵按一下您要停用的索引，然後選取 [停用]。  
  
6.  在 **[停用索引]** 對話方塊中，確認 **[要停用的索引]** 方格中有正確索引，然後按一下 **[確定]**。  
  
#### <a name="to-disable-all-indexes-on-a-table"></a>停用資料表上的所有索引  
  
1.  在 [物件總管] 中，按一下加號展開資料庫，此資料庫包含您要停用索引的資料表。  
  
2.  按一下加號展開 **[資料表]** 資料夾。  
  
3.  按一下加號展開要停用索引的資料表。  
  
4.  以滑鼠右鍵按一下 [索引] 資料夾，並選取 [全部停用]。  
  
5.  在 **[停用索引]** 對話方塊中，確認 **[要停用的索引]** 方格中有正確索引，然後按一下 **[確定]**。 若要從 **[要停用的索引]** 方格中移除索引，請選取索引，然後按下 DELETE 鍵。  
  
 **[停用索引]** 對話方塊中提供下列資訊：  
  
 **Index Name**  
 顯示索引的名稱。 在執行期間，此資料行也會顯示代表其狀態的圖示。  
  
 **資料表名稱**  
 顯示建立索引的資料表名稱或檢視名稱。  
  
 **索引類型**  
 顯示索引的類型：[叢集]、[非叢集]、[空間] 或 [XML]。  
  
 **狀態**  
 顯示停用作業的狀態。 執行之後可能的值：  
  
-   空白  
  
     執行之前 **[狀態]** 為空白。  
  
-   **進行中**  
  
     已經開始停用索引，但尚未完成。  
  
-   **成功**  
  
     已成功地完成停用作業。  
  
-   **錯誤**  
  
     停用索引作業期間發生錯誤，未成功地完成作業。  
  
-   **Stopped**  
  
     因為使用者停止作業，所以未成功地完成停用索引。  
  
 **訊息**  
 提供停用作業期間錯誤訊息的文字。 在執行期間，會以超連結顯示錯誤。 超連結的文字會描述錯誤的主體。 **[訊息]** 資料行通常寬度不足以讀取完整訊息文字。 取得完整文字有兩種方式：  
  
-   將滑鼠指標移至訊息資料格上，即可顯示具有錯誤文字的工具提示。  
  
-   按一下超連結即可顯示含有完整錯誤的對話方塊。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-disable-an-index"></a>若要停用索引  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- disables the IX_Employee_OrganizationLevel_OrganizationNode index  
    -- on the HumanResources.Employee table  
    ALTER INDEX IX_Employee_OrganizationLevel_OrganizationNode ON HumanResources.Employee  
    DISABLE;  
    ```  
  
#### <a name="to-disable-all-indexes-on-a-table"></a>停用資料表上的所有索引  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Disables all indexes on the HumanResources.Employee table.  
    ALTER INDEX ALL ON HumanResources.Employee  
    DISABLE;  
    ```  
  
 如需詳細資訊，請參閱 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)。  
  
  
