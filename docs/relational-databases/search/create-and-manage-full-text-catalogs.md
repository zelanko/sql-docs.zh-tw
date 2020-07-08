---
title: 建立及管理全文檢索目錄 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text catalogs [SQL Server], creating
- full-text search [SQL Server], using SQL Server Management Studio
ms.assetid: 824b7131-44a6-4815-89e6-62b7bab060e3
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6999d409c81f19e0a8ae3903fe220e0c75235c8d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85678681"
---
# <a name="create-and-manage-full-text-catalogs"></a>建立及管理全文檢索目錄
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
全文檢索目錄是一組全文檢索索引的邏輯容器。 您必須先建立全文檢索目錄，才能建立全文檢索索引。

全文檢索目錄是不屬於任何檔案群組的虛擬物件。
  
##  <a name="create-a-full-text-catalog"></a><a name="creating"></a> 建立全文檢索目錄  

### <a name="create-a-full-text-catalog-with-transact-sql"></a>使用 Transact-SQL 建立全文檢索目錄
使用 [CREATE FULLTEXT CATALOG](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)。 例如：

```sql 
USE AdventureWorks;  
GO  
CREATE FULLTEXT CATALOG ftCatalog AS DEFAULT;  
GO  
``` 

### <a name="create-a-full-text-catalog-with-management-studio"></a>使用 Management Studio 建立全文檢索目錄
1.  在物件總管中，展開伺服器，並展開 [資料庫]  ，然後展開您要在其中建立全文檢索目錄的資料庫。  
  
2.  展開 [儲存體]  ，然後以滑鼠右鍵按一下 [全文檢索目錄]  。  
  
3.  選取 [新增全文檢索目錄]  。  
  
4.  在 [新增全文檢索目錄]  對話方塊中，為您要重新建立的目錄指定資訊。 如需詳細資訊，請參閱[全文檢索搜尋](/sql/database-engine/new-full-text-catalog-general-page)。  
  
    > [!NOTE]  
    >  全文檢索目錄識別碼從 00005 開始，每次新增一個目錄時識別碼便增加一號。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

##  <a name="get-the-properties-of-a-full-text-catalog"></a><a name="props"></a> 取得全文檢索目錄的屬性  
使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函式 **FULLTEXTCATALOGPROPERTY** 取得各種全文檢索目錄相關屬性的值。 如需詳細資訊，請參閱 [FULLTEXTCATALOGPROPERTY](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md)。

例如，執行下列查詢來取得全文檢索目錄 `Catalog1` 中的索引計數。

```sql 
USE <database>;  
GO  
SELECT fulltextcatalogproperty('Catalog1', 'ItemCount');  
GO  
```  
  
下表列出與全文檢索目錄相關的屬性。 此資訊適用於管理全文檢索搜尋並對其進行疑難排解。 
  
|屬性|描述|  
|--------------|-----------------|  
|**AccentSensitivity**|區分腔調字設定。|
|**ImportStatus**|是否正在匯入全文檢索目錄。|  
|**IndexSize**|全文檢索目錄的大小 (以 MB 為單位)。| 
|**ItemCount**|目前在全文檢索目錄中的全文檢索索引項目數。|  
|**MergeStatus**|主要合併是否正在進行中。| 
|**PopulateCompletionAge**|前次全文檢索索引母體擴展完成和 01/01/1990 00:00:00 之間的時差 (以秒為單位)。| 
|**PopulateStatus**|擴展狀態。<br /><br /> [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]|  
|**UniqueKeyCount**|全文檢索目錄中唯一索引鍵的數目。| 

##  <a name="rebuild-a-full-text-catalog"></a><a name="rebuildone"></a> 重建全文檢索目錄  

執行 Transact-SQL 陳述式 [ALTER FULLTEXT CATALOG ...REBUILD](
../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)，或在 SQL Server Management Studio (SSMS) 中執行下列事項。

1.  在 SSMS 中，於物件總管中，展開伺服器，並展開 [資料庫]  ，然後展開含有您要重建其全文檢索目錄的資料庫。  
  
2.  展開 [儲存體]  ，然後展開 [全文檢索目錄]  。  
  
3.  以滑鼠右鍵按一下要重建的全文檢索目錄名稱，然後選取 [重建]  。  
  
4.  出現 [您要刪除全文檢索目錄，並重建目錄嗎?]  問題時，按一下 [確定]  。  
  
5.  在 [重建全文檢索目錄]  對話方塊中，按一下 [關閉]  。  
   
##  <a name="rebuild-all-full-text-catalogs-for-a-database"></a><a name="rebuildall"></a> 重建資料庫的所有全文檢索目錄  

1.  在 SSMS 中，於物件總管中，展開伺服器，並展開 [資料庫]  ，然後展開含有您要重建之全文檢索目錄的資料庫。  
  
2.  展開 [儲存體]  ，然後以滑鼠右鍵按一下 [全文檢索目錄]  。  
  
3.  選取 [全部重建]  。  
  
4.  出現 [您要刪除所有全文檢索目錄，並重建這些目錄嗎?]  問題時，按一下 [確定]  。  
  
5.  在 [重建所有全文檢索目錄]  對話方塊中，按一下 [關閉]  。  
  
  
  
##  <a name="remove-a-full-text-catalog-from-a-database"></a><a name="removing"></a> 從資料庫移除全文檢索目錄  

執行 Transact-SQL 陳述式 [DROP FULLTEXT CATALOG](
../../t-sql/statements/drop-fulltext-catalog-transact-sql.md)，或在 SQL Server Management Studio (SSMS) 中執行下列事項。

1.  在 SSMS 中，於物件總管中，依序展開伺服器、[資料庫]  ，並展開含有您要移除之全文檢索目錄的資料庫。  
  
2.  展開 [儲存體]  ，再展開 [全文檢索目錄]  。  
  
3.  以滑鼠右鍵按一下要移除的全文檢索目錄，然後選取 [刪除]  。  
  
4.  在 **[刪除物件]** 對話方塊中，按一下 **[確定]** 。  

## <a name="next-step"></a>後續步驟
[建立及管理全文檢索索引](../../relational-databases/search/create-and-manage-full-text-indexes.md)
