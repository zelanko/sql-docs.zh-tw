---
title: 記憶體最佳化資料表的統計資料 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: e644766d-1d1c-43d7-83ff-8ccfe4f3af9f
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1a15c617c2be877c19d447d615261a6d38eae9eb
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718951"
---
# <a name="statistics-for-memory-optimized-tables"></a>記憶體最佳化資料表的統計資料
  查詢最佳化工具會使用有關資料行的統計資料來建立可改善查詢效能的查詢計劃。 統計資料是從資料庫中的資料表收集，並且儲存在資料庫中繼資料內。  
  
 統計資料是自動建立的，但也可以手動建立。 例如，建立索引時就會自動建立索引鍵資料行的統計資料。 如需有關建立統計資料的詳細資訊，請參閱 [統計資料](../statistics/statistics.md)。  
  
 資料表資料通常會隨資料列插入、更新和刪除而變更。 這表示，統計資料需要定期更新。 根據預設，以磁碟為基礎的資料表上的統計資料會在最佳化工具判斷統計資料可能過期時自動更新。  
  
 根據預設，記憶體最佳化資料表上的統計資料不會更新。 您需要手動更新這些統計資料。 針對個別資料行、索引或資料表，請使用[UPDATE STATISTICS &#40;transact-sql&#41;](/sql/t-sql/statements/update-statistics-transact-sql) 。 使用[sp_updatestats &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql)來更新資料庫中所有使用者和內部資料表的統計資料。  
  
 當您使用[CREATE statistics &#40;transact-sql&#41;](/sql/t-sql/statements/create-statistics-transact-sql)或[UPDATE statistics &#40;transact-sql&#41;](/sql/t-sql/statements/update-statistics-transact-sql)時，您必須指定 `NORECOMPUTE` 來停用記憶體優化資料表的自動統計資料更新。 對於以磁片為基礎的資料表，只有在上次[sp_updatestats &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql)之後修改資料表時， [sp_updatestats &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql)才會更新統計資料。 對於記憶體優化資料表， [sp_updatestats &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql)一律會產生更新的統計資料。 [sp_updatestats &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql)是記憶體優化資料表的理想選項;否則，您必須知道哪些資料表有重大變更，才能個別更新統計資料。  
  
 可以藉由取樣資料或執行完整掃描來產生統計資料。 取樣的統計資料只會使用資料表資料的取樣來估計資料分佈情形。 完整掃描的統計資料會掃描整個資料表來判斷資料分佈情形。 完整掃描的統計資料通常更正確，但要花較多的時間來計算。 取樣的統計資料收集速度較快。  
  
 以磁碟為基礎的資料表預設為使用取樣的統計資料。 記憶體最佳化資料表只支援完整掃描統計資料。 使用[CREATE statistics &#40;transact-sql&#41;](/sql/t-sql/statements/create-statistics-transact-sql)或[&#40;TRANSACT-SQL&#41;更新統計資料](/sql/t-sql/statements/update-statistics-transact-sql)時，您必須指定 `FULLSCAN` 記憶體優化資料表的選項。  
  
 記憶體最佳化資料表上統計資料的額外考量：  
  
-   記憶體最佳化資料表上的索引會隨資料表建立。 索引鍵資料行上的統計資料會在資料表為空白時建立。 因此，這些統計資料需要在資料載入資料表後更新。  
  
-   若是原生編譯預存程序，程序中查詢的執行計畫會在編譯程序時最佳化。 這種情況只會在建立程序及伺服器重新啟動時發生，而不會在統計資料更新時發生。 因此，資料表需要包含代表性的資料集，且統計資料需要處於最新狀態，才能建立程序  (如果讓資料庫離線後再次上線，或有任何伺服器重新啟動，則原生編譯的預存程序會重新編譯)。  
  
## <a name="guidelines-for-statistics-when-deploying-memory-optimized-tables"></a>部署記憶體最佳化資料表時統計資料的方針  
 為確保查詢最佳化工具建立查詢計劃時擁有最新的統計資料，請利用下列五個步驟部署記憶體最佳化資料表：  
  
1.  建立資料表及索引。 索引是在 `CREATE TABLE` 陳述式中以內嵌方式指定。  
  
2.  將資料載入資料表中。  
  
3.  更新資料表上的統計資料。  
  
4.  建立存取資料表的預存程序。  
  
5.  執行工作負載，其中包含混合原生編譯和解譯的 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 預存程序以及特定批次。  
  
 在您載入資料並更新統計資料後建立原生編譯預存程序，可確保最佳化工具能夠提供統計資料給記憶體最佳化資料表。 這樣將可確保編譯程序時，查詢計劃能夠保持效率。  
  
## <a name="guidelines-for-maintaining-statistics-on-memory-optimized-tables"></a>維護記憶體最佳化資料表上統計資料的方針  
 為了讓統計資料保持最新狀態，請定期更新記憶體最佳化資料表上的統計資料。  
  
 如果資料經常變更，則應經常更新統計資料。 例如，在批次更新後更新資料表統計資料。 在您更新統計資料後，卸除並重新建立原生編譯預存程序，讓程序能夠利用更新的統計資料。  
  
 .  
  
 不要在尖峰工作負載期間更新統計資料。  
  
 若要更新統計資料：  
  
-   用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 來建立具有[更新統計](../maintenance-plans/update-statistics-task-maintenance-plan.md)資料[工作的維護計畫](../maintenance-plans/create-a-maintenance-plan.md)  
  
-   或是透過 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 指令碼更新統計資料，如下列所討論。  
  
 若要更新單一記憶體優化資料表的統計資料（*myschema*。 *Mytable*），請執行下列腳本：  
  
```  
UPDATE STATISTICS myschema.Mytable WITH FULLSCAN, NORECOMPUTE  
```  
  
 若要更新目前資料庫中所有記憶體最佳化資料表的統計資料，請執行下列指令碼：  
  
```sql  
DECLARE @sql NVARCHAR(MAX) = N''  
  
SELECT @sql += N'  
   UPDATE STATISTICS ' + quotename(schema_name(schema_id)) + N'.' + quotename(name) + N' WITH FULLSCAN, NORECOMPUTE'  
FROM sys.tables WHERE is_memory_optimized=1  
  
EXEC sp_executesql @sql  
```  
  
 若要更新資料庫中所有資料表的統計資料，請執行[sp_updatestats &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql)。  
  
 下列範例會報告記憶體最佳化資料表的統計資料上次更新時間。 這項資訊可協助您決定是否需要更新統計資料。  
  
```sql  
select t.object_id, t.name, sp.last_updated as 'stats_last_updated'  
from sys.tables t join sys.stats s on t.object_id=s.object_id cross apply sys.dm_db_stats_properties(t.object_id, s.stats_id) sp  
where t.is_memory_optimized=1  
```  
  
## <a name="see-also"></a>另請參閱  
 [記憶體最佳化資料表](memory-optimized-tables.md)  
  
  
