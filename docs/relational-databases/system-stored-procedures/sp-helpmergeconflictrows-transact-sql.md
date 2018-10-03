---
title: sp_helpmergeconflictrows (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergeconflictrows_TSQL
- sp_helpmergeconflictrows
helpviewer_keywords:
- sp_helpmergeconflictrows
ms.assetid: 131395a5-cb18-4795-a7ae-fa09d8ff347f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 26bf2e89462c0096c9a6fd2a081cb72c68e9a32a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47746576"
---
# <a name="sphelpmergeconflictrows-transact-sql"></a>sp_helpmergeconflictrows (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 [ **@publication=**] **'***publication***'**  
 這是發行集的名稱。 *發行集*已**sysname**，預設值是**%**。 如果指定發行集的話，就會傳回發行集所限定的所有衝突。 比方說，如果**MSmerge_conflict_Customers**資料表中有衝突資料列**WA**並**CA**發行集，在發行集名稱中傳遞**CA**擷取相關衝突**CA**發行集。  
  
 [  **@conflict_table=**] **'***conflict_table***'**  
 這是衝突資料表的名稱。 *conflict_table*已**sysname**，沒有預設值。 在  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]及更新版本中，衝突資料表會使用命名與格式名稱 **MSmerge_conflict_* 發行集 *_* 文章 * 中，使用一個資料表針對每個發行發行項。  
  
 [ **@publisher=**] **'***publisher***'**  
 這是發行者的名稱。 *發行者*已**sysname**，預設值是 NULL。  
  
 [ **@publisher_db=**] **'***publisher_db***'**  
 是發行者資料庫的名稱。*publisher_db*是**sysname**，預設值是 NULL。  
  
 [  **@logical_record_conflicts=** ] *logical_record_conflicts&lt*  
 指出結果集是否包含有關邏輯記錄衝突的資訊。 *logical_record_conflicts&lt*已**int**，預設值為 0。 **1**表示會傳回邏輯記錄衝突資訊。  
  
## <a name="result-sets"></a>結果集  
 **sp_helpmergeconflictrows**傳回的結果集的基底資料表結構和這些額外的資料行所組成。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**origin_datasource**|**varchar(255)**|衝突的來源。|  
|**conflict_type**|**int**|衝突類型的代碼：<br /><br /> **1** = 更新衝突： 在資料列層級偵測到衝突。<br /><br /> **2** = 資料行更新衝突： 資料行層級偵測到衝突。<br /><br /> **3** = 更新刪除成功衝突： 刪除在衝突中獲勝。<br /><br /> **4** = 更新成功刪除衝突： 衝突失敗已刪除的 rowguid 會記錄在此資料表。<br /><br /> **5** = 上傳插入失敗： 訂閱者的插入無法套用在發行者端。<br /><br /> **6** = 下載插入失敗： 發行者的插入無法套用在訂閱者。<br /><br /> **7** = 上傳刪除失敗： 訂閱者端刪除無法上傳到 「 發行者 」。<br /><br /> **8** = 下載刪除失敗： 發行者的刪除無法下載到訂閱者。<br /><br /> **9** = 上傳更新失敗： 無法在發行者端套用訂閱者端的更新。<br /><br /> **10** = 下載更新失敗： 發行者端的更新無法套用到訂閱者。<br /><br /> **12** = 邏輯記錄更新成功刪除： 刪除在衝突中失敗的邏輯記錄會記錄在此資料表。<br /><br /> **13** = 邏輯記錄衝突插入更新： 插入邏輯記錄衝突的更新。<br /><br /> **14** = 邏輯記錄刪除成功更新衝突： 衝突失敗更新的邏輯記錄會記錄在此資料表。|  
|**reason_code**|**int**|可為內容相關的錯誤碼。|  
|**reason_text**|**varchar(720)**|可為內容相關的錯誤描述。|  
|**pubid**|**uniqueidentifier**|發行集識別碼。|  
|**MSrepl_create_time**|**datetime**|加入衝突資訊的時間。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_helpmergeconflictrows**用於合併式複寫中。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定伺服器角色**db_owner**固定資料庫角色，而**replmonitor**散發資料庫中的角色可以執行**sp_helpmergeconflictrows**。  
  
## <a name="see-also"></a>另請參閱  
 [檢視合併式發行集的衝突資訊&#40;複寫 TRANSACT-SQL 程式設計&#41;](../../relational-databases/replication/view-conflict-information-for-merge-publications.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
