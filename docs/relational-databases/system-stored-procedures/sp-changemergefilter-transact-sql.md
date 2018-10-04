---
title: sp_changemergefilter (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_changemergefilter_TSQL
- sp_changemergefilter
helpviewer_keywords:
- sp_changemergefilter
ms.assetid: e08fdfdd-d242-4e85-817b-9f7a224fe567
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1d43af8f9ffc64eb7fcfaba5aff7434696376321
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47704846"
---
# <a name="spchangemergefilter-transact-sql"></a>sp_changemergefilter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  變更部分合併篩選屬性。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_changemergefilter [ @publication= ] 'publication'  
        , [ @article= ] 'article'  
        , [ @filtername= ] 'filtername'  
        , [ @property= ] 'property'  
        , [ @value= ] 'value'  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@publication=** ] **'***發行集***'**  
 這是發行集的名稱。 *發行集*已**sysname**，沒有預設值。  
  
 [  **@article=** ] **'***文章***'**  
 這是發行項的名稱。 *發行項*已**sysname**，沒有預設值。  
  
 [  **@filtername=** ] **'***filtername***'**  
 這是目前篩選的名稱。 *filtername*已**sysname**，沒有預設值。  
  
 [  **@property=** ] **'***屬性***'**  
 這是要變更的屬性名稱。 *屬性*已**sysname**，沒有預設值。  
  
 [  **@value=**] **'***值***'**  
 這是指定之屬性的新值。 *值*已**nvarchar(1000)**，沒有預設值。  
  
 下表描述發行項的屬性及這些屬性的值。  
  
|屬性|值|描述|  
|--------------|-----------|-----------------|  
|**filter_type**|**1**|聯結篩選。<br /><br /> 支援 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 訂閱者需要這個選項。|  
||**2**|邏輯記錄關聯性。|  
||**3**|聯結篩選也是一項邏輯記錄關聯性。|  
|**filtername**||篩選的名稱。|  
|**join_articlename**||聯結發行項的名稱。|  
|**join_filterclause**||篩選子句。|  
|**join_unique_key**|**true**|聯結作用於唯一索引鍵|  
||**false**|聯結不作用於唯一索引鍵|  
  
 [  **@force_invalidate_snapshot =** ] *force_invalidate_snapshot*  
 認可這個預存程序所採取的動作可能使現有的快照集失效。 *force_invalidate_snapshot*已**位元**，預設值**0**。  
  
 **0**指定合併發行項的變更不會使快照集失效。 如果預存程序偵測到變更需要新的快照集，就會發生錯誤，且不會進行任何變更。  
  
 **1**表示的合併發行項的變更可能使快照集失效，而且如果有現有的訂閱需要新的快照集，提供要標示為已棄用之現有快照集產生新的快照集的權限。  
  
 [  **@force_reinit_subscription =** ] *force_reinit_subscription*  
 認可這個預存程序所採取的動作可能需要重新初始化現有的訂閱。 *force_reinit_subscription*已**位元**預設值是**0**。  
  
 **0**指定合併發行項的變更不會使訂閱重新初始化。 如果預存程序偵測到變更需要重新初始化現有的訂閱，就會發生錯誤，且不會進行任何變更。  
  
 **1**表示合併發行項的變更會導致現有的訂閱重新初始化，並提供發生之訂閱重新初始化的權限。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_changemergefilter**用於合併式複寫中。  
  
 如果快照集存在的話，變更合併發行項的篩選需要重新建立快照集。 這藉由設定**@force_invalidate_snapshot**要**1**。 另外，如果有這個發行項的訂閱，也必須重新初始化訂閱。 這是藉由設定**@force_reinit_subscription**要**1**。  
  
 若要使用邏輯記錄，發行集和發行項必須符合許多需求。 如需詳細資訊，請參閱[使用邏輯記錄分組相關資料列的變更](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_changemergefilter**。  
  
## <a name="see-also"></a>另請參閱  
 [變更發行集與發行項屬性](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [sp_addmergefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md)   
 [sp_dropmergefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergefilter-transact-sql.md)   
 [sp_helpmergefilter &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-helpmergefilter-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
