---
description: sp_helpmergeconflictrows (Transact-SQL)
title: sp_helpmergeconflictrows (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergeconflictrows_TSQL
- sp_helpmergeconflictrows
helpviewer_keywords:
- sp_helpmergeconflictrows
ms.assetid: 131395a5-cb18-4795-a7ae-fa09d8ff347f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 4c66dc9c8ac6cc21d74cbf2a6474ad74a2cffba1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88485937"
---
# <a name="sp_helpmergeconflictrows-transact-sql"></a>sp_helpmergeconflictrows (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  傳回指定衝突資料表中的資料列。 這個預存程序是在儲存了衝突資料表的電腦中執行的。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helpmergeconflictrows [ [ @publication = ] 'publication' ]  
        , [ @conflict_table = ] 'conflict_table'  
    [ , [ @publisher = ] 'publisher' ]   
    [ , [ @publisher_db = ] 'publsher_db' ]   
    [ , [ @logical_record_conflicts = ] logical_record_conflicts ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'` 這是發行集的名稱。 *發行* 集是 **sysname**，預設值是 **%** 。 如果指定發行集的話，就會傳回發行集所限定的所有衝突。 例如，如果 **MSmerge_conflict_Customers** 資料表具有適用于 **WA** 和 **ca** 發行集的衝突資料列，則在發行集名稱 **ca** 中傳遞會抓取與 **ca** 發行集相關的衝突。  
  
`[ @conflict_table = ] 'conflict_table'` 這是衝突資料表的名稱。 *conflict_table* 是 **sysname**，沒有預設值。 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本中，衝突資料表的命名方式是使用**MSmerge_conflict \_ _ \_ 發行_** 項的格式名稱，以及每個已發行之發行項的資料表。  
  
`[ @publisher = ] 'publisher'` 這是發行者的名稱。 *publisher* 是 **sysname**，預設值是 Null。  
  
`[ @publisher_db = ] 'publisher_db'` 這是發行者資料庫的名稱。*publisher_db* 是 **sysname**，預設值是 Null。  
  
`[ @logical_record_conflicts = ] logical_record_conflicts` 指出結果集是否包含有關邏輯記錄衝突的資訊。 *logical_record_conflicts* 是 **int**，預設值是0。 **1** 表示會傳回邏輯記錄衝突資訊。  
  
## <a name="result-sets"></a>結果集  
 **sp_helpmergeconflictrows** 會傳回結果集，其中包含基表結構和這些額外的資料行。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**origin_datasource**|**varchar(255)**|衝突的來源。|  
|**conflict_type**|**int**|衝突類型的代碼：<br /><br /> **1** = 更新衝突：在資料列層級偵測到衝突。<br /><br /> **2** = 資料行更新衝突：在資料行層級偵測到衝突。<br /><br /> **3** = 更新刪除獲勝衝突：刪除在衝突中獲勝。<br /><br /> **4** = 更新 Wins 刪除衝突：遺失衝突的已刪除 rowguid 會記錄在此資料表中。<br /><br /> **5** = 上傳插入失敗：訂閱者的插入無法套用在發行者端。<br /><br /> **6** = 下載插入失敗：無法在訂閱者端套用來自發行者的插入。<br /><br /> **7** = 上傳刪除失敗：訂閱者端的刪除無法上傳至發行者。<br /><br /> **8** = 下載刪除失敗：發行者端的刪除無法下載到訂閱者。<br /><br /> **9** = 上傳更新失敗：訂閱者端的更新無法套用在發行者端。<br /><br /> **10** = 下載更新失敗：「發行者」端的更新無法套用至「訂閱者」。<br /><br /> **12** = 邏輯記錄更新獲勝刪除：遺失衝突的已刪除邏輯記錄會記錄在此資料表中。<br /><br /> **13** = 邏輯記錄衝突插入更新：對邏輯記錄的插入與更新衝突。<br /><br /> **14** = 邏輯記錄刪除 Wins 更新衝突：遺失衝突的更新邏輯記錄會記錄在此資料表中。|  
|**reason_code**|**int**|可為內容相關的錯誤碼。|  
|**reason_text**|**Varchar (720) **|可為內容相關的錯誤描述。|  
|**pubid**|**uniqueidentifier**|發行集識別碼。|  
|**MSrepl_create_time**|**datetime**|加入衝突資訊的時間。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_helpmergeconflictrows** 用於合併式複寫中。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色、 **db_owner** 固定資料庫角色，以及散發資料庫中的 **replmonitor** 角色的成員，才能夠執行 **sp_helpmergeconflictrows**。  
  
## <a name="see-also"></a>另請參閱  
 [查看合併式發行集的衝突資訊 &#40;複寫 Transact-sql 程式設計&#41;](../../relational-databases/replication/view-conflict-information-for-merge-publications.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
