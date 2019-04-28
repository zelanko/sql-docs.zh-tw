---
title: sp_createstats (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_createstats_TSQL
- sp_createstats
dev_langs:
- TSQL
helpviewer_keywords:
- sp_createstats
ms.assetid: 8204f6f2-5704-40a7-8d51-43fc832eeb54
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a32df85b1a2b7362a22c27d05f68c07cf32a3200
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62724453"
---
# <a name="spcreatestats-transact-sql"></a>sp_createstats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  呼叫[CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md)還不是統計資料物件中的第一個資料行的資料行上建立單一資料行統計資料的陳述式。 建立單一資料行統計資料會增加長條圖的數目，而且可能會改善基數估計值、查詢計劃和查詢效能。 統計資料物件的第一個資料行具有長條圖，但其他資料行則沒有長條圖。  
  
 當查詢執行時間很重要而且無法等候查詢最佳化工具產生單一資料行統計資料時，sp_createstats 對於效能評定等應用程式會很有用。 在大部分情況下，它不需要使用 sp_createstats;查詢最佳化工具產生單一資料行統計資料，以便改善查詢計劃的時機**AUTO_CREATE_STATISTICS**選項是否開啟。  
  
 如需統計資料的詳細資訊，請參閱[統計資料](../../relational-databases/statistics/statistics.md)。 如需有關產生單一資料行統計資料的詳細資訊，請參閱 < **AUTO_CREATE_STATISTICS**選項[ALTER DATABASE SET 選項&#40;-&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_createstats   
    [   [ @indexonly =   ] { 'indexonly'   | 'NO' } ]   
    [ , [ @fullscan =    ] { 'fullscan'    | 'NO' } ]   
    [ , [ @norecompute = ] { 'norecompute' | 'NO' } ]  
    [ , [ @incremental = ] { 'incremental' | 'NO' } ]  
```  
  
## <a name="arguments"></a>引數  
`[ @indexonly = ] 'indexonly'` 只有位於現有索引並不是任何索引定義中的第一個資料行的資料行建立統計資料。 **indexonly**已**char(9)**。 預設值是 NO。  
  
`[ @fullscan = ] 'fullscan'` 會使用[CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md)陳述式搭配**FULLSCAN**選項。 **fullscan**已**char(9)**。  預設值是 NO。  
  
`[ @norecompute = ] 'norecompute'` 會使用[CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md)陳述式搭配**NORECOMPUTE**選項。 **norecompute**已**char(12)**。  預設值是 NO。  
  
`[ @incremental = ] 'incremental'` 會使用[CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md)陳述式搭配**INCREMENTAL = ON**選項。 **累加**已**char(12)**。  預設值是 NO。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 每個新的統計資料物件都與建立時所在的資料行具有相同的名稱。  
  
## <a name="remarks"></a>備註  
 sp_createstats 不會建立或更新現有的統計資料物件，第一個資料行的資料行的統計資料 這包括建立索引、 具有使用 AUTO_CREATE_STATISTICS 選項所產生的單一資料行統計資料的資料行和使用 CREATE STATISTICS 陳述式建立的統計資料的第一個資料行的統計資料的第一個資料行。 sp_createstats 不會停用的索引的第一個資料行上建立統計資料，除非該資料行用於其他已啟用索引。 sp_createstats 不會包含已停用叢集索引的資料表上建立統計資料。  
  
 當此資料表包含資料行集時，sp_createstats 就不會建立疏鬆資料行的統計資料。 如需有關資料行集和疏鬆資料行的詳細資訊，請參閱 <<c0> [ 使用資料行集](../../relational-databases/tables/use-column-sets.md)並[使用疏鬆資料行](../../relational-databases/tables/use-sparse-columns.md)。  
  
## <a name="permissions"></a>Permissions  
 需要 db_owner 固定資料庫角色中的成員資格。  
  
## <a name="examples"></a>範例  
  
### <a name="a-create-single-column-statistics-on-all-eligible-columns"></a>A. 針對所有適合的資料行建立單一資料行統計資料  
 下列範例會針對目前資料庫中所有適合的資料行建立單一資料行統計資料。  
  
```  
EXEC sp_createstats;  
GO  
```  
  
### <a name="b-create-single-column-statistics-on-all-eligible-index-columns"></a>B. 針對所有適合的索引資料行建立單一資料行統計資料  
 下列範例會針對已經位於索引中而且不是索引中第一個資料行的所有適合資料行建立單一資料行統計資料。  
  
```  
EXEC sp_createstats 'indexonly';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [統計資料](../../relational-databases/statistics/statistics.md)   
 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [ALTER DATABASE SET 選項 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [Database Engine 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
