---
title: sp_helpmergearticle （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergearticle
- sp_helpmergearticle_TSQL
helpviewer_keywords:
- sp_helpmergearticle
ms.assetid: 0fb9986a-3c33-46ef-87bb-297396ea5a6a
author: stevestein
ms.author: sstein
ms.openlocfilehash: e1c297e050121c3013242c40938fdd4c0ba8b936
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68122338"
---
# <a name="sp_helpmergearticle-transact-sql"></a>sp_helpmergearticle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回發行項的相關資訊。 這個預存程序執行於發行集資料庫的發行者端，或訂閱資料庫的重新發行訂閱者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helpmergearticle [ [ @publication = ] 'publication' ]  
    [ , [ @article= ] 'article' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'`這是要取得資訊的發行集名稱。 *發行*集是**sysname**，預設值是**%**，它會傳回目前資料庫中所有發行集所包含之所有合併發行項的相關資訊。  
  
`[ @article = ] 'article'`這是要傳回信息的發行項名稱。 發行項**sysname** **%** 是 sysname，預設值是，它會傳回給定發行集中所有合併發行項的相關資訊。 *article*  
  
## <a name="result-set"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**id**|**int**|發行項識別碼。|  
|**name**|**sysname**|發行項的名稱。|  
|**source_owner**|**sysname**|來源物件擁有者的名稱。|  
|**source_object**|**sysname**|新增發行項的來源物件名稱。|  
|**sync_object_owner**|**sysname**|定義已發行的發行項之檢視的擁有者名稱。|  
|**sync_object**|**sysname**|用來建立資料分割初始資料之自訂物件的名稱。|  
|**描述**|**nvarchar(255)**|發行項的描述。|  
|**status**|**tinyint**|發行項的狀態，它可以是下列項目之一：<br /><br /> **1** = 非使用中<br /><br /> **2** = 使用中<br /><br /> **5** = 資料定義語言（DDL）作業暫止<br /><br /> **6** = 使用新產生之快照集的 DDL 作業<br /><br /> 注意：重新初始化發行項時， **5**和**6**的值會變更為**2**。|  
|**creation_script**|**nvarchar(255)**|在訂閱資料庫中，用來建立發行項的選擇性發行項結構描述指令碼的路徑和名稱。|  
|**conflict_table**|**Nvarchar （270）**|儲存插入或更新衝突的資料表名稱。|  
|**article_resolver**|**nvarchar(255)**|自訂的發行項解析程式。|  
|**subset_filterclause**|**nvarchar(1000)**|指定水平篩選的 WHERE 子句。|  
|**pre_creation_command**|**tinyint**|預先建立方法，它可以是下列項目之一：<br /><br /> **0** = 無<br /><br /> **1** = drop<br /><br /> **2** = 刪除<br /><br /> **3** = 截斷|  
|**schema_option**|**binary （8）**|發行項的結構描述產生選項點陣圖。 如需這個點陣圖選項的詳細資訊，請參閱[sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)或[sp_changemergearticle](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)。|  
|**type**|**smallint**|發行項的類型，它可以是下列項目之一：<br /><br /> **10** = 資料表<br /><br /> **32** = 預存程式<br /><br /> **64** = view 或 indexed view<br /><br /> **128** = 使用者定義函數<br /><br /> **160** = 僅限同義字架構|  
|**column_tracking**|**int**|資料行層級追蹤的設定;其中**1**表示資料行層級追蹤是 on，而**0**表示資料行層級的追蹤已關閉。|  
|**resolver_info**|**nvarchar(255)**|發行項解析程式的名稱。|  
|**vertical_partition**|**bit**|如果發行項是垂直分割，則為，其中**1**表示發行項是垂直分割，而**0**表示不是。|  
|**destination_owner**|**sysname**|目的地物件的擁有者。 只適用於合併預存程序、檢視和使用者自訂函數 (UDF) 結構描述發行項。|  
|**identity_support**|**int**|如果已啟用自動識別範圍處理，則為，其中**1**已啟用，而**0**已停用。|  
|**pub_identity_range**|**bigint**|當指派新的識別值時，所用的範圍大小。 如需詳細資訊，請參閱複寫[識別欄位](../../relational-databases/replication/publish/replicate-identity-columns.md)的「合併式複寫」一節。|  
|**identity_range**|**bigint**|當指派新的識別值時，所用的範圍大小。 如需詳細資訊，請參閱複寫[識別欄位](../../relational-databases/replication/publish/replicate-identity-columns.md)的「合併式複寫」一節。|  
|**閾值**|**int**|執行[!INCLUDE[ssEW](../../includes/ssew-md.md)]或舊版的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]訂閱者所使用的百分比值。 當合併代理程式指派新的識別範圍時，**臨界值**控制。 當使用 threshold 指定的百分比值，合併代理程式會建立新的識別範圍。 如需詳細資訊，請參閱複寫[識別欄位](../../relational-databases/replication/publish/replicate-identity-columns.md)的「合併式複寫」一節。|  
|**verify_resolver_signature**|**int**|如果在合併式複寫中使用解析程式之前先驗證數位簽章，則為，其中**0**表示不會驗證簽章，而**1**表示會驗證簽章，以查看它是否來自信任的來源。|  
|**destination_object**|**sysname**|目的地物件的名稱。 只適用於合併預存程序、檢視和 UDF 結構描述發行項。|  
|**allow_interactive_resolver**|**int**|如果在發行項上使用互動式解析程式，則為，其中**1**表示使用此解析程式， **0**表示不使用它。|  
|**fast_multicol_updateproc**|**int**|啟用或停用合併代理程式，將變更套用至一個 UPDATE 語句中相同資料列的多個資料行;其中**1**表示在一個語句中更新多個資料行，而**0**表示個別的 UPDATE 語句會針對每個更新的資料行發出問題。|  
|**check_permissions**|**int**|這是一個整數值，代表所驗證之資料表層級權限的點陣圖。 如需可能值的清單，請參閱[sp_addmergearticle &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。|  
|**processing_order**|**int**|發行集中的發行項套用資料變更的順序。|  
|**upload_options**|**tinyint**|定義客訂閱在訂閱者端進行的更新之限制，它可以是下列值之一。<br /><br /> **0** = 在訂閱者上使用用戶端訂閱所進行的更新沒有任何限制;所有變更都會上傳到發行者。<br /><br /> **1** = 具有用戶端訂閱的訂閱者可以進行變更，但是不會上傳至發行者。<br /><br /> **2** = 在具有用戶端訂閱的訂閱者上不允許變更。<br /><br /> 如需詳細資訊，請參閱[使用僅限下載的發行項最佳化合併式複寫效能](../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)。|  
|**identityrangemanagementoption**|**int**|如果已啟用自動識別範圍處理，則為，其中**1**已啟用，而**0**已停用。|  
|**delete_tracking**|**bit**|如果已複寫刪除，則為，其中**1**表示已複寫刪除， **0**表示不會複寫。|  
|**compensate_for_errors**|**bit**|指出在同步處理期間發生錯誤時，是否採取補償動作;其中**1**表示採取補償動作， **0**表示不採取補償動作。|  
|**partition_options**|**tinyint**|定義發行項資料進行資料分割的方式，當所有資料列只屬於單一資料分割或單一訂閱時，能夠使效能最佳化。 *partition_options*可以是下列其中一個值。<br /><br /> **0** = 發行項的篩選是靜態的，或不產生每個分割區的唯一資料子集;也就是說，它是一個「重迭」的資料分割。<br /><br /> **1** = 分割區重迭，而在訂閱者端進行的資料操作語言（DML）更新，無法變更資料列所屬的分割區。<br /><br /> **2** = 發行項的篩選會產生非重迭的資料分割，但多個訂閱者可以接收相同的資料分割。<br /><br /> **3** = 發行項的篩選會產生對每個訂閱而言都是唯一的非重迭資料分割。|  
|**artid**|**uniqueidentifier**|唯一識別發行項的識別碼。|  
|**pubid**|**uniqueidentifier**|唯一識別發行項發行在其中之發行集的識別碼。|  
|**stream_blob_columns**|**bit**|這是指當複寫二進位大型物件資料行時，是否使用資料流最佳化。 **1**表示正在使用優化， **0**表示不使用優化。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_helpmergearticle**用於合併式複寫中。  
  
## <a name="permissions"></a>權限  
 只有發行集資料庫中**db_owner**固定資料庫角色的成員、散發資料庫中的**replmonitor**角色，或發行集的發行集存取清單，才可以執行**sp_helpmergearticle**。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_helpmergearticle](../../relational-databases/replication/codesnippet/tsql/sp-helpmergearticle-tran_1.sql)]  
  
## <a name="see-also"></a>另請參閱  
 [查看和修改發行項屬性](../../relational-databases/replication/publish/view-and-modify-article-properties.md)   
 [sp_addmergearticle &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)   
 [sp_changemergearticle &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [sp_dropmergearticle &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
