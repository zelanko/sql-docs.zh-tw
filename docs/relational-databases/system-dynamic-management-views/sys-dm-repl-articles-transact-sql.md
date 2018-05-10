---
title: sys.dm_repl_articles (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_repl_articles_TSQL
- dm_repl_articles
- dm_repl_articles_TSQL
- sys.dm_repl_articles
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_repl_articles dynamic management function
ms.assetid: 794d514e-bacd-432e-a8ec-3a063a97a37b
caps.latest.revision: 16
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4d1e7ccd9f4bc09bde7ac3be680356b8e93a3827
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmreplarticles-transact-sql"></a>sys.dm_repl_articles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳送有關在複寫拓撲中以發行項發行之資料庫物件的資訊。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**artcache_db_address**|**varbinary(8)**|發行集資料庫之快取資料庫結構的記憶體中位址。|  
|**artcache_table_address**|**varbinary(8)**|已發行之資料表發行項的快取資料表結構的記憶體中位址。|  
|**artcache_schema_address**|**varbinary(8)**|已發行之資料表發行項的快取發行項結構描述結構的記憶體中位址。|  
|**artcache_article_address**|**varbinary(8)**|已發行之資料表發行項的快取發行項結構的記憶體中位址。|  
|**artid**|**bigint**|唯一識別這份資料表內的每一個項目。|  
|**artfilter**|**bigint**|用來水平篩選發行項之預存程序的識別碼。|  
|**artobjid**|**bigint**|已發行物件的識別碼。|  
|**artpubid**|**bigint**|發行集所屬發行集的識別碼。|  
|**artstatus**|**tinyint**|發行項選項和狀態的位元遮罩，它可能是一或多個這些值的位元邏輯 OR 結果：<br /><br /> **1** = 發行項在使用中。<br /><br /> **8** = 資料行名稱包括在 INSERT 陳述式。<br /><br /> **16** = 使用參數化陳述式。<br /><br /> **24** = 這包括在 INSERT 陳述式的資料行名稱，並使用參數化陳述式。<br /><br /> 例如，對於使用參數化陳述式的使用中發行項，這個資料行的值是 17。 0 值表示發行項不在使用中，且未定義任何其他屬性。|  
|**arttype**|**tinyint**|發行項類型：<br /><br /> **1** = 記錄式發行項。<br /><br /> **3** = 含有手動篩選記錄檔為基礎的發行項。<br /><br /> **5** = 含有手動檢視的記錄式發行項。<br /><br /> **7** = 含有手動篩選和手動檢視的記錄式發行項。<br /><br /> **8** = 預存程序執行。<br /><br /> **24** = 可序列化的預存程序執行。<br /><br /> **32** = 預存程序 （僅限結構描述）。<br /><br /> **64** = 檢視 （僅限結構描述）。<br /><br /> **128** = 函式 （僅限結構描述）。|  
|**wszArtdesttable**|**nvarchar(514)**|目的地的已發行物件名稱。|  
|**wszArtdesttableowner**|**nvarchar(514)**|目的地的已發行物件擁有者。|  
|**wszArtinscmd**|**nvarchar(510)**|用於插入的命令或預存程序。|  
|**cmdTypeIns**|**int**|用於插入預存程序的呼叫語法，它可以是下列值之一。<br /><br /> **1** = 呼叫<br /><br /> **2** = SQL<br /><br /> **3** = 無<br /><br /> **7** = 未知|  
|**wszArtdelcmd**|**nvarchar(510)**|用於刪除的命令或預存程序。|  
|**cmdTypeDel**|**int**|用於刪除預存程序的呼叫語法，它可以是下列值之一。<br /><br /> **0** = XCALL<br /><br /> **1** = 呼叫<br /><br /> **2** = SQL<br /><br /> **3** = 無<br /><br /> **7** = 未知|  
|**wszArtupdcmd**|**nvarchar(510)**|用於更新的命令或預存程序。|  
|**cmdTypeUpd**|**int**|用於更新預存程序的呼叫語法，它可以是下列值之一。<br /><br /> **0** = XCALL<br /><br /> **1** = 呼叫<br /><br /> **2** = SQL<br /><br /> **3** = 無<br /><br /> **4** = MCALL<br /><br /> **5** = VCALL<br /><br /> **6** = SCALL<br /><br /> **7** = 未知|  
|**wszArtpartialupdcmd**|**nvarchar(510)**|用於部分更新的命令或預存程序。|  
|**cmdTypePartialUpd**|**int**|用於部分更新預存程序的呼叫語法，它可以是下列值之一。<br /><br /> **2** = SQL|  
|**numcol**|**int**|用於垂直篩選發行項之資料分割中的資料行數目。|  
|**artcmdtype**|**tinyint**|目前複寫的命令類型，它可以是下列值之一。<br /><br /> **1** = 插入<br /><br /> **2** = 刪除<br /><br /> **3** = 更新<br /><br /> **4** = UPDATETEXT<br /><br /> **5** = 無<br /><br /> **6** = 僅供內部使用<br /><br /> **7** = 僅供內部使用<br /><br /> **8** = 部分 UPDATE|  
|**artgeninscmd**|**nvarchar(510)**|以發行項包含的資料行為基礎之 INSERT 命令範本。|  
|**artgendelcmd**|**nvarchar(510)**|DELETE 命令範本可包含發行項所包含的主索引鍵或資料行，隨著使用的呼叫語法而不同。|  
|**artgenupdcmd**|**nvarchar(510)**|UPDATE 命令範本可包含主索引鍵、更新的資料行或完整資料行清單，隨著使用的呼叫語法而不同。|  
|**artpartialupdcmd**|**nvarchar(510)**|部分 UPDATE 命令範本，它包含主索引鍵和更新的資料行。|  
|**artupdtxtcmd**|**nvarchar(510)**|UPDATETEXT 命令範本，它包含主索引鍵和更新的資料行。|  
|**artgenins2cmd**|**nvarchar(510)**|在並行快照集處理期間，重新調整發行項時使用的 INSERT 命令範本。|  
|**artgendel2cmd**|**nvarchar(510)**|在並行快照集處理期間，重新調整發行項時使用的 DELETE 命令範本。|  
|**fInReconcile**|**tinyint**|指出在並行快照集處理期間，目前是否重新調整發行項。|  
|**fPubAllowUpdate**|**tinyint**|指出發行集是否允許更新訂閱。|  
|**intPublicationOptions**|**bigint**|指定其他發行選項的點陣圖，位元選項值如下：<br /><br /> **0x1** -啟用端對端複寫。<br /><br /> **0x2** -只發行本機變更。<br /><br /> **0x4** -已啟用的非 SQL Server 訂閱者。|  
  
## <a name="permissions"></a>Permissions  
 需要 VIEW DATABASE STATE 權限在發行集資料庫上的呼叫**dm_repl_articles**。  
  
## <a name="remarks"></a>備註  
 只對目前載入複寫發行項快取中的複寫資料庫物件傳回這項資訊。  
  
## <a name="see-also"></a>另請參閱  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [複寫相關的動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/replication-related-dynamic-management-views-transact-sql.md)  
  
  

