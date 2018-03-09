---
title: "sp_helparticle (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_helparticle_TSQL
- sp_helparticle
helpviewer_keywords:
- sp_helparticle
ms.assetid: 9c4a1a88-56f1-45a0-890c-941b8e0f0799
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 823862d782cafd605dd7f4686dcdb3b4baa6a0b8
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="sphelparticle-transact-sql"></a>sp_helparticle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  顯示發行項的相關資訊。 這個預存程序執行於發行集資料庫的發行者端。 如果是 Oracle 發行者，這個預存程序執行於任何資料庫中的散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helparticle [ @publication = ] 'publication'   
    [ , [ @article = ] 'article' ]  
    [ , [ @returnfilter = ] returnfilter ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @found = ] found OUTPUT ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@publication =**] **'***發行集***'**  
 這是發行集的名稱。 *發行集*是**sysname**，沒有預設值。  
  
 [  **@article=**] **'***文章***'**  
 這是發行集的發行項名稱。 *發行項*是**sysname**，預設值是 **%** 。 如果*文章*是未提供，會傳回指定之發行集的所有發行項的相關資訊。  
  
 [  **@returnfilter=**] *returnfilter*  
 指定是否應該傳回篩選子句。 *returnfilter*是**元**，預設值是**1**，它會傳回篩選子句。  
  
 [  **@publisher** =] **'***發行者***'**  
 指定非[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。 *發行者*是**sysname**，預設值是 NULL。  
  
> [!NOTE]  
>  *發行者*不應指定當要求資訊的發行項上發行的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。  
  
 [  **@found=** ]*找到*輸出  
 僅供內部使用。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**發行項識別碼**|**int**|發行項的識別碼。|  
|**發行項名稱**|**sysname**|發行項的名稱。|  
|**基底物件**|**nvarchar （257)**|發行項或預存程序所代表之基礎資料表的名稱。|  
|**目的地物件**|**sysname**|目的地 (訂閱) 資料表的名稱。|  
|**同步處理物件**|**nvarchar （257)**|定義已發行的發行項之檢視的名稱。|  
|**型別**|**smallint**|發行項的類型：<br /><br /> **1** = 記錄檔為基礎。<br /><br /> **3** = 含有手動篩選的記錄檔為基礎。<br /><br /> **5** = 含有手動檢視記錄檔型。<br /><br /> **7** = 含有手動篩選和手動檢視記錄檔型。<br /><br /> **8** = 預存程序執行。<br /><br /> **24** = 可序列化的預存程序執行。<br /><br /> **32** = 預存程序 （僅限結構描述）。<br /><br /> **64** = 檢視 （僅限結構描述）。<br /><br /> **96** = 彙總函式 （僅限結構描述）。<br /><br /> **128** = 函式 （僅限結構描述）。<br /><br /> **257** = 記錄式索引檢視表。<br /><br /> **超過 259** = 含有手動篩選記錄式索引檢視表。<br /><br /> **261** = 含有手動檢視記錄式索引檢視表。<br /><br /> **263** = 含有手動篩選記錄式索引檢視表和手動檢視。<br /><br /> **320** = 索引檢視表 （僅限結構描述）。<br /><br />|  
|**status**|**tinyint**|可以是[& (位元 AND)](../../t-sql/language-elements/bitwise-and-transact-sql.md)結果的一個或多個這些發行項屬性：<br /><br /> **0x00** = [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> **0x01** = 發行項在使用中。<br /><br /> **0x08** = 資料行名稱包括在 insert 陳述式。<br /><br /> **0x16** = 使用參數化陳述式。<br /><br /> **0x32** = 使用參數化陳述式和 insert 陳述式中包含的資料行名稱。|  
|**filter**|**nvarchar （257)**|用來水平篩選資料表的預存程序。 必須已利用 FOR REPLICATION 子句來建立這個預存程序。|  
|**描述**|**nvarchar(255)**|發行項的描述項目。|  
|**insert_command**|**nvarchar(255)**|當隨著資料表發行項而複寫插入時，所用的複寫命令類型。 如需詳細資訊，請參閱[指定交易式發行項變更的傳播方式](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)。|  
|**update_command**|**nvarchar(255)**|當隨著資料表發行項而複寫更新時，所用的複寫命令類型。 如需詳細資訊，請參閱[指定交易式發行項變更的傳播方式](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)。|  
|**delete_command**|**nvarchar(255)**|當隨著資料表發行項而複寫刪除時，所用的複寫命令類型。 如需詳細資訊，請參閱[指定交易式發行項變更的傳播方式](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)。|  
|**建立指令碼路徑**|**nvarchar(255)**|用來建立目標資料表之發行項結構描述指令碼的路徑和名稱。|  
|**垂直資料分割**|**bit**|是否垂直資料分割是否啟用發行項。值**1**表示啟用垂直資料分割。|  
|**pre_creation_cmd**|**tinyint**|DROP TABLE、DELETE TABLE 或 TRUNCATE 的預先建立命令：|  
|**filter_clause**|**ntext**|指定水平篩選的 WHERE 子句。|  
|**schema_option**|**binary （8)**|給定發行項的結構描述產生選項點陣圖。 如需完整的清單**schema_option**值，請參閱[sp_addarticle &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md).|  
|**dest_owner**|**sysname**|目的地物件的擁有者名稱。|  
|**source_owner**|**sysname**|來源物件的擁有者。|  
|**unqua_source_object**|**sysname**|來源物件的名稱，不含擁有者名稱。|  
|**sync_object_owner**|**sysname**|定義已發行的發行項之檢視的擁有者。 執行個體時提供 SQL Server 登入。|  
|**unqualified_sync_object**|**sysname**|定義已發行的發行項之檢視的名稱，不含擁有者名稱。|  
|**filter_owner**|**sysname**|篩選的擁有者。|  
|**unqua_filter**|**sysname**|篩選的名稱，不含擁有者名稱。|  
|**auto_identity_range**|**int**|這是一個旗標，指出在前次建立發行集時，開啟了自動識別範圍處理。 **1**表示啟用自動識別範圍。**0**表示已停用。|  
|**publisher_identity_range**|**int**|如果發行項的範圍內的 「 發行者 」 端的識別範圍大小*identityrangemanagementoption*設**自動**或**auto_identity_range**設**true**。|  
|**identity_range**|**bigint**|如果發行項的範圍內的 「 訂閱者 」 端的識別範圍大小*identityrangemanagementoption*設**自動**或**auto_identity_range**設**true**。|  
|**臨界值**|**bigint**|這是一個百分比值，指出散發代理程式指派新識別範圍的時機。|  
|**identityrangemanagementoption**|**int**|指出處理發行項的識別範圍管理。|  
|**fire_triggers_on_snapshot**|**bit**|這是指在套用初始快照集時，是否執行複寫的使用者觸發程序。<br /><br /> **1** = 執行觸發程序的使用者。<br /><br /> **0** = 不執行觸發程序的使用者。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_helparticle**用於快照式複寫和異動複寫。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定伺服器角色、 **db_owner**固定的資料庫角色或目前發行集的發行集存取清單可以執行**sp_helparticle**.  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_helptranarticle](../../relational-databases/replication/codesnippet/tsql/sp-helparticle-transact-_1.sql)]  
  
## <a name="see-also"></a>請參閱＜  
 [檢視和修改發行項屬性](../../relational-databases/replication/publish/view-and-modify-article-properties.md)   
 [sp_addarticle &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articlecolumn &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
