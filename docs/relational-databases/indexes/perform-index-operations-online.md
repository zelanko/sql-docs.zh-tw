---
title: "線上執行索引作業 | Microsoft Docs"
ms.custom: 
ms.date: 02/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.technology: dbe-indexes
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- index online operations [SQL Server]
- online index operations
- ONLINE option
ms.assetid: 1e43537c-bf67-4db3-9908-3cb45c6fdaa1
caps.latest.revision: 32
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.suite: SQL
ms.prod_service: database engine, sql database, sql data warehouse
ms.component: indexes
ms.translationtype: HT
ms.sourcegitcommit: bc1321dd91a0fcb7ab76b207301c6302bb3a5e64
ms.openlocfilehash: c2a7e07e2af46446f9271eb82d1dae13f6da2145
ms.contentlocale: zh-tw
ms.lasthandoff: 10/06/2017

---
# <a name="perform-index-operations-online"></a>線上執行索引作業
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中線上建立、重建或卸除索引。 在這些索引作業期間，ONLINE 選項可讓並行使用者存取基礎資料表或叢集索引資料，以及任何關聯的非叢集索引。 例如，當某個使用者正在重建叢集索引時，此使用者和其他人可以繼續更新和查詢基礎資料。 當您離線執行資料定義語言 (DDL) 作業 (例如建立或重建叢集索引) 時，這些作業會保有基礎資料和關聯索引的獨佔鎖定。 這可避免在索引作業完成之前對基礎資料進行修改和查詢。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的所有版本都無法使用線上索引作業。 如需詳細資訊，請參閱＜SQL Server 2016 版本支援的功能＞。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要線上重建索引，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   建議您針對全年無休的商務環境執行線上索引作業，在索引作業期間，這類環境的並行使用者活動需求相當重要。  
  
-   ONLINE 選項可用於下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。  
  
    -   [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md)  
  
    -   [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md)  
  
    -   [DROP INDEX](../../t-sql/statements/drop-index-transact-sql.md)  
  
    -   [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) (搭配 CLUSTERED 索引選項時，用來加入或卸除 UNIQUE 或 PRIMARY KEY 條件約束)  
  
-   如需更多有關線上建立、重建或卸除索引的限制，請參閱 [線上索引作業的指導方針](../../relational-databases/indexes/guidelines-for-online-index-operations.md)。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 需要資料表或檢視表的 ALTER 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-rebuild-an-index-online"></a>若要線上重建索引  
  
1.  在 [物件總管] 中，按一下加號展開包含您要線上重建索引之資料表的資料庫。  
  
2.  展開 **[資料表]** 資料夾。  
  
3.  按一下加號展開要線上重建索引的資料表。  
  
4.  展開 **[索引]** 資料夾。  
  
5.  以滑鼠右鍵按一下要線上重建的索引，然後選取 [屬性]。  
  
6.  在 **[選取頁面]**底下，選取 **[選項]**。  
  
7.  選取 **[允許線上 DML 處理]**，然後從清單中選取 **[True]** 。  
  
8.  按一下 **[確定]**。  
  
9. 以滑鼠右鍵按一下要線上重建的索引，然後選取 [重建]。  
  
10. 在 **[重建索引]** 對話方塊中，確認 **[要重建的索引]** 方格中有正確索引，然後按一下 **[確定]**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-rebuild-or-drop-an-index-online"></a>若要線上建立、重建或卸除索引  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。 這個範例會線上重建現有索引  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    ALTER INDEX AK_Employee_NationalIDNumber ON HumanResources.Employee  
    REBUILD WITH (ONLINE = ON);  
    GO  
    ```  
  
     下列範例會在線上刪除叢集索引，並利用 `NewGroup` 子句，將產生的資料表 (堆積) 移到 `MOVE TO` 檔案群組。 它會查詢 `sys.indexes`、 `sys.tables`和 `sys.filegroups` 目錄檢視來確認在移動之前和之後，索引和資料表在檔案群組中的位置。  
  
     [!code-sql[IndexDDL#DropIndex4](../../relational-databases/indexes/codesnippet/tsql/perform-index-operations_1.sql)]  
  
 如需詳細資訊，請參閱 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)。  
  
  

