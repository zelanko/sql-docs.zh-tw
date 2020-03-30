---
title: 修改索引 | Microsoft Docs
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- indexes [SQL Server], modifying
- modifying indexes
- index changes [SQL Server]
ms.assetid: 97e3110d-fde7-4f5d-9309-dc1697960aeb
author: MikeRayMSFT
ms.author: mikeray
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 9c8334573b66b5c227a5033a63b5aedf06909c78
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "68316964"
---
# <a name="modify-an-index"></a>修改索引
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，修改 [!INCLUDE[tsql](../../includes/tsql-md.md)]中的索引。  
  
> [!IMPORTANT]  
>  因 PRIMARY KEY 或 UNIQUE 條件約束而建立的索引將無法使用此方法來修改。 必須修改條件約束。  
  
 **本主題內容**  
  
-   **若要修改索引，使用：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-modify-an-index"></a>若要修改索引  
  
1.  在 [物件總管] 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的執行個體，然後展開該執行個體。  
  
2.  展開 **[資料庫]** ，展開資料表所在的資料庫，然後展開 **[資料表]** 。  
  
3.  展開索引所在的資料表，然後展開 **[索引]** 。  
  
4.  以滑鼠右鍵按一下您要修改的索引，然後按一下 [屬性]  。  
  
5.  在 **[索引屬性]** 對話方塊中，進行所需的變更。 例如，您可以在索引鍵中加入或移除資料行，或是變更索引選項的設定。  
  
#### <a name="to-modify-index-columns"></a>若要修改索引資料行  
  
1.  若要加入、移除或變更索引資料行的位置，請選取 **[索引屬性]** 對話方塊中的 **[一般]** 頁面。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-modify-an-index"></a>若要修改索引  
  
下列範例會利用 `ProductID` 選項，在 AdventureWorks 資料庫中 `Production.WorkOrder` 資料表的 `DROP_EXISTING` 資料行上卸除並重新建立現有的索引。 也會設定 `FILLFACTOR` 和 `PAD_INDEX` 選項。  
  
[!code-sql[IndexDDL#CreateIndex4](../../relational-databases/indexes/codesnippet/tsql/modify-an-index_1.sql)]  
  
下列範例會使用 ALTER INDEX 設定 `AK_SalesOrderHeader_SalesOrderNumber`索引的幾個選項。  
  
[!code-sql[IndexDDL#AlterIndex4](../../relational-databases/indexes/codesnippet/tsql/modify-an-index_2.sql)]  
  
#### <a name="to-modify-index-columns"></a>若要修改索引資料行  
  
1.  若要加入、移除或變更索引資料行的位置，您必須卸除索引，再重新建立該索引。  
  
## <a name="see-also"></a>另請參閱  
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
 [INDEXPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/indexproperty-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [設定索引選項](../../relational-databases/indexes/set-index-options.md)   
 [重新命名索引](../../relational-databases/indexes/rename-indexes.md)  
  
  
