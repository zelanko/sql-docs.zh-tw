---
title: sp_updatestats （Transact-sql） |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e28564c44dc226054f0b08e8ba75fe36509cf064
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82808919"
---
# <a name="sp_updatestats-transact-sql"></a>sp_updatestats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

`UPDATE STATISTICS`針對目前資料庫中的所有使用者定義和內部資料表執行。  
  
如需的詳細資訊 `UPDATE STATISTICS` ，請參閱[&#40;Transact-sql&#41;更新統計資料](../../t-sql/statements/update-statistics-transact-sql.md)。 如需統計資料的詳細資訊，請參閱[統計資料](../../relational-databases/statistics/statistics.md)。  
    
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
sp_updatestats [ [ @resample = ] 'resample']  
```  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="arguments"></a>引數  
`[ @resample = ] 'resample'`指定**sp_updatestats**將使用[UPDATE STATISTICS](../../t-sql/statements/update-statistics-transact-sql.md)語句的 [重新取樣] 選項。 如果未指定 [重新**取樣**]， **sp_updatestats**會使用預設取樣來更新統計資料。 重新**取樣**是**Varchar （8）** ，預設值是 NO。  
  
## <a name="remarks"></a>備註  
 **sp_updatestats**會藉 `UPDATE STATISTICS` 由 `ALL` 在資料庫中的所有使用者定義和內部資料表上指定關鍵字來執行。 sp_updatestats 會顯示指出其進度的訊息。 當更新完成時，它會報告已更新所有資料表的統計資料。  
  
sp_updatestats 會針對停用的非叢集索引更新統計資料，但不會針對停用的叢集索引更新統計資料。  
  
對於以磁片為基礎的資料表， **sp_updatestats**會根據**sys.databases dm_db_stats_properties**目錄檢視中的**modification_counter**資訊更新統計資料，並更新至少一個資料列已修改的統計資料。 執行**sp_updatestats**時，一定會更新記憶體優化資料表的統計資料。 因此，請勿執行**sp_updatestats**超過所需。  
  
**sp_updatestats**可以觸發預存程式或其他已編譯器代碼的重新編譯。 不過，如果參考的資料表和其上的索引只有一個查詢計劃，則**sp_updatestats**可能不會導致重新編譯。 在這些情況下，重新編譯是不必要的，即使已更新統計資料也一樣。  
  
對於相容性層級低於90的資料庫，執行**sp_updatestats**並不會保留特定統計資料的最新 NORECOMPUTE 設定。 對於相容性層級為90或更高的資料庫，sp_updatestats 會保留特定統計資料的最新 NORECOMPUTE 選項。 如需停用及重新啟用統計資料更新的詳細資訊，請參閱[統計資料](../../relational-databases/statistics/statistics.md)。  
  
## <a name="permissions"></a>權限  
 需要**系統管理員（sysadmin** ）固定伺服器角色中的成員資格，或資料庫（**dbo**）的擁有權。  

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
 [&#40;Transact-sql&#41;建立統計資料](../../t-sql/statements/create-statistics-transact-sql.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-sql&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS &#40;Transact-sql&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [sp_autostats &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-autostats-transact-sql.md)   
 [sp_createstats &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-createstats-transact-sql.md)   
 [更新 &#40;Transact-sql&#41;的統計資料](../../t-sql/statements/update-statistics-transact-sql.md)   
 [系統預存程式](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
 
