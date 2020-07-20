---
title: 線上執行索引作業 | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- index online operations [SQL Server]
- online index operations
- ONLINE option
ms.assetid: 1e43537c-bf67-4db3-9908-3cb45c6fdaa1
author: MikeRayMSFT
ms.author: mikeray
ms.prod_service: table-view-index, sql-database
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 10561f70eaed5aad48e62f0cd4e87a1c2851bcbe
ms.sourcegitcommit: 7ce4a81c1b91239c8871c50f97ecaf387f439f6c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2020
ms.locfileid: "86217776"
---
# <a name="perform-index-operations-online"></a>線上執行索引作業
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  此主題描述如何使用 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中線上建立、重建或卸除索引。 在這些索引作業期間，ONLINE 選項可讓並行使用者存取基礎資料表或叢集索引資料，以及任何關聯的非叢集索引。 例如，當某個使用者正在重建叢集索引時，此使用者和其他人可以繼續更新和查詢基礎資料。 當您離線執行資料定義語言 (DDL) 作業 (例如建立或重建叢集索引) 時，這些作業會保有基礎資料和關聯索引的獨佔鎖定。 這可避免在索引作業完成之前對基礎資料進行修改和查詢。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的所有版本都無法使用線上索引作業。 如需詳細資訊，請參閱 [SQL Server 的版本及支援功能](../../sql-server/editions-and-components-of-sql-server-version-15.md)。 
>
> 您可在 Azure SQL Database 中使用線上索引作業。
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要線上重建索引，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
  
-   建議您針對全年無休的商務環境執行線上索引作業，在索引作業期間，這類環境的並行使用者活動需求相當重要。  
  
-   ONLINE 選項可用於下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。  
  
    -   [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md)  
  
    -   [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md)  
  
    -   [DROP INDEX](../../t-sql/statements/drop-index-transact-sql.md)  
  
    -   [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) (搭配 CLUSTERED 索引選項時，用來加入或卸除 UNIQUE 或 PRIMARY KEY 條件約束)  
  
-   如需更多有關線上建立、重建或卸除索引的限制，請參閱 [線上索引作業的指導方針](../../relational-databases/indexes/guidelines-for-online-index-operations.md)。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 需要資料表或檢視表的 ALTER 權限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-rebuild-an-index-online"></a>若要線上重建索引  
  
1.  在 [物件總管] 中，按一下加號展開包含您要線上重建索引之資料表的資料庫。  
  
2.  展開 **[資料表]** 資料夾。  
  
3.  按一下加號展開要線上重建索引的資料表。  
  
4.  展開 **[索引]** 資料夾。  
  
5.  以滑鼠右鍵按一下要線上重建的索引，然後選取 [屬性]。  
  
6.  在 **[選取頁面]** 底下，選取 **[選項]** 。  
  
7.  選取 **[允許線上 DML 處理]** ，然後從清單中選取 **[True]** 。  
  
8.  按一下 [確定]。  
  
9. 以滑鼠右鍵按一下要線上重建的索引，然後選取 [重建]。  
  
10. 在 **[重建索引]** 對話方塊中，確認 **[要重建的索引]** 方格中有正確索引，然後按一下 **[確定]** 。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
### <a name="to-create-rebuild-or-drop-an-index-online"></a>若要線上建立、重建或卸除索引  
  
下列範例會在 AdventureWorks 資料庫中重建現有線上索引。

```sql
ALTER INDEX AK_Employee_NationalIDNumber
    ON HumanResources.Employee
    REBUILD WITH (ONLINE = ON);
```  
  
下列範例會在線上刪除叢集索引，並利用 `NewGroup` 子句，將產生的資料表 (堆積) 移到 `MOVE TO` 檔案群組。 它會查詢 `sys.indexes`、 `sys.tables`和 `sys.filegroups` 目錄檢視來確認在移動之前和之後，索引和資料表在檔案群組中的位置。  
  
[!code-sql[IndexDDL#DropIndex4](../../relational-databases/indexes/codesnippet/tsql/perform-index-operations_1.sql)]  

如需詳細資訊，請參閱 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)。

## <a name="next-steps"></a>後續步驟

- [可繼續索引考量因素](guidelines-for-online-index-operations.md#resumable-index-considerations)
