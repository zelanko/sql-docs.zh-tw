---
description: sp_updatestats (Transact-SQL)
title: sp_updatestats (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 09/25/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_updatestats_TSQL
- sp_updatestats
dev_langs:
- TSQL
helpviewer_keywords:
- sp_updatestats
ms.assetid: 01184651-6e61-45d9-a502-366fecca0ee4
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f976f9be51d688833a09e5faaae42b8864ecc274
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97482380"
---
# <a name="sp_updatestats-transact-sql"></a>sp_updatestats (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

`UPDATE STATISTICS`針對目前資料庫中的所有使用者自訂和內部資料表執行。  
  
如需的詳細資訊 `UPDATE STATISTICS` ，請參閱 [&#40;Transact-sql&#41;更新統計資料 ](../../t-sql/statements/update-statistics-transact-sql.md)。 如需統計資料的詳細資訊，請參閱[統計資料](../../relational-databases/statistics/statistics.md)。  
    
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
sp_updatestats [ [ @resample = ] 'resample']  
```  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="arguments"></a>引數  
`[ @resample = ] 'resample'` 指定 **sp_updatestats** 將使用 [UPDATE STATISTICS](../../t-sql/statements/update-statistics-transact-sql.md) 語句的重新取樣選項。 如果未指定「重新 **取樣** 」， **sp_updatestats** 會使用預設取樣來更新統計資料。 重新 **取樣** 是 **Varchar (8)** 預設值為 NO。  
  
## <a name="remarks"></a>備註  
 **sp_updatestats** 會 `UPDATE STATISTICS` `ALL` 在資料庫中的所有使用者定義和內部資料表上指定關鍵字來執行。 sp_updatestats 顯示指出其進度的訊息。 當更新完成時，它會報告已更新所有資料表的統計資料。  
  
**sp_updatestats** 更新已停用之非叢集索引的統計資料，而且不會更新已停用之叢集索引的統計資料  
  
若是以磁片為基礎的資料表， **sp_updatestats** 會根據 **sys.dm_db_stats_properties** 類別目錄檢視中 **modification_counter** 資訊更新統計資料，以更新至少一個資料列已修改的統計資料。 執行 **sp_updatestats** 時，一定會更新記憶體優化資料表的統計資料。 因此，不需要執行 **sp_updatestats** 。  
  
**sp_updatestats** 可以觸發預存程式或其他已編譯器代碼的重新編譯。 不過，如果參考的資料表和索引上的索引只有一個查詢計劃， **sp_updatestats** 可能不會造成重新編譯。 在這些情況下，重新編譯是不必要的，即使已更新統計資料也一樣。  
  
針對相容性層級低於90的資料庫，執行 **sp_updatestats** 不會保留特定統計資料的最新 NORECOMPUTE 設定。 針對相容性層級為90或更高的資料庫，sp_updatestats 會保留特定統計資料的最新 NORECOMPUTE 選項。 如需停用及重新啟用統計資料更新的詳細資訊，請參閱[統計資料](../../relational-databases/statistics/statistics.md)。  
  
## <a name="permissions"></a>權限  

若要執行 **sp_updatestats**，使用者必須是資料庫 (的擁有者，而 `dbo` 不只是角色的成員 `db_owner`) 或是系統管理員（sysadmin）固定伺服器角色的成員。

## <a name="examples"></a>範例  
下列範例會更新 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫中之資料表的統計資料。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_updatestats;   
```  

## <a name="automatic-index-and-statistics-management"></a>自動索引與統計資料管理
利用[自適性索引重組](https://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag)等解決方案，為一或多個資料庫自動管理索引重組以及統計資料更新。 這項程序會根據索引分散程度與其他參數，自動選擇要進行重建或是重新組織索引，並以線性閾值更新統計資料。

## <a name="see-also"></a>另請參閱  
 [ALTER DATABASE SET 選項 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [sp_autostats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-autostats-transact-sql.md)   
 [sp_createstats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-createstats-transact-sql.md)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [系統預存程式](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
 
