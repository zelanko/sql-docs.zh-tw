---
title: "sys.sysindexes (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-compatibility-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysindexes
- sysindexes_TSQL
- sys.sysindexes
- sys.sysindexes_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sysindexes system table
- sys.sysindexes compatibility view
ms.assetid: f483d89c-35c4-4a08-8f8b-737fd80d13f5
caps.latest.revision: "57"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 4d196e511921980543b23c45c36ada1a6f1eba41
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="syssysindexes-transact-sql"></a>sys.sysindexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  針對目前資料庫中每個索引和資料表，各包含一個資料列。 這份檢視不支援 XML 索引。 資料分割的資料表和索引不完全支援在這個檢視中。使用[sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)目錄檢視。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**id**|**int**|索引所屬的資料表識別碼。|  
|**status**|**int**|系統狀態資訊。<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**第一個**|**binary(6)**|指向第一個頁面或根頁面的指標。<br /><br /> 當**indid** = 0。<br /><br /> NULL = 索引已分割時**indid** > 1。<br /><br /> NULL = 資料表已分割時**indid**是 0 或 1。|  
|**indid**|**smallint**|索引的識別碼：<br /><br /> 0 = 堆積<br /><br /> 1 = 叢集索引<br /><br /> > 1 = 非叢集索引|  
|**根**|**binary(6)**|如**indid** > = 1，**根**根頁面的指標。<br /><br /> 當**indid** = 0。<br /><br /> NULL = 索引已分割時**indid** > 1。<br /><br /> NULL = 資料表已分割時**indid**是 0 或 1。|  
|**minlen**|**smallint**|資料列的大小下限。|  
|**keycnt**|**smallint**|索引鍵數目。|  
|**groupid**|**smallint**|建立物件的檔案群組識別碼。<br /><br /> NULL = 索引已分割時**indid** > 1。<br /><br /> NULL = 資料表已分割時**indid**是 0 或 1。|  
|**dpages**|**int**|如**indid** = 0 或**indid** = 1， **dpages**是所使用的資料頁的計數。<br /><br /> 如**indid** > 1， **dpages**是索引所使用的頁面計數。<br /><br /> 0 = 索引已分割時**indid** > 1。<br /><br /> 0 = 資料表已分割時**indid**是 0 或 1。<br /><br /> 如果發生資料列溢位，便不產生精確的結果。|  
|**保留**|**int**|如**indid** = 0 或**indid** = 1，**保留**是頁面配置之所有索引和資料表的資料計數。<br /><br /> 如**indid** > 1，**保留**是索引所配置的頁面計數。<br /><br /> 0 = 索引已分割時**indid** > 1。<br /><br /> 0 = 資料表已分割時**indid**是 0 或 1。<br /><br /> 如果發生資料列溢位，便不產生精確的結果。|  
|**使用**|**int**|如**indid** = 0 或**indid** = 1，**用**是用於所有索引和資料表資料的總頁數計數。<br /><br /> 如**indid** > 1，**用**是針對索引所使用的頁面計數。<br /><br /> 0 = 索引已分割時**indid** > 1。<br /><br /> 0 = 資料表已分割時**indid**是 0 或 1。<br /><br /> 如果發生資料列溢位，便不產生精確的結果。|  
|**rowcnt**|**bigint**|基礎資料層級資料列計數**indid** = 0 和**indid** = 1。<br /><br /> 0 = 索引已分割時**indid** > 1。<br /><br /> 0 = 資料表已分割時**indid**是 0 或 1。|  
|**rowmodctr**|**int**|計算前次更新資料表的統計資料之後，插入、刪除或更新資料列的總數。<br /><br /> 0 = 索引已分割時**indid** > 1。<br /><br /> 0 = 資料表已分割時**indid**是 0 或 1。<br /><br /> 在[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]和更新版本， **rowmodctr**不完全與舊版相容。 如需詳細資訊，請參閱＜備註＞。|  
|**reserved3**|**int**|傳回 0。<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**reserved4**|**int**|傳回 0。<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xmaxlen**|**smallint**|資料列的大小上限|  
|**maxirow**|**smallint**|非分葉索引資料列的大小上限。<br /><br /> 在[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]和更新版本， **maxirow**不完全與舊版相容。|  
|**OrigFillFactor**|**tinyint**|當建立索引時，所用的原始填滿因數值。 這個值並沒有維護；不過，如果您必須重建索引，且忘了所用的填滿因數值，它可能很有用。|  
|**StatVersion**|**tinyint**|傳回 0。<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**reserved2**|**int**|傳回 0。<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**FirstIAM**|**binary(6)**|NULL = 索引進行分割。<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**impid**|**smallint**|索引實作旗標。<br /><br /> 傳回 0。<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**lockflags**|**smallint**|用來約束所考量的索引鎖定資料粒度。 例如，若要將鎖定成本降到最低，您可以將基本上是唯讀的參考表設為只執行資料表層級的鎖定。|  
|**pgmodctr**|**int**|傳回 0。<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**索引鍵**|**varbinary(816)**|組成索引鍵的各個資料行之資料行識別碼清單。<br /><br /> 傳回 NULL。<br /><br /> 若要顯示索引鍵資料行，請使用[sys.sysindexkeys](../../relational-databases/system-compatibility-views/sys-sysindexkeys-transact-sql.md)。|  
|**name**|**sysname**|索引或統計資料的名稱。 傳回 NULL **indid** = 0。 請修改您的應用程式來查閱 NULL 堆積名稱。|  
|**statblob**|**image**|統計資料二進位大型物件 (BLOB)。<br /><br /> 傳回 NULL。|  
|**maxlen**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**資料列**|**int**|基礎資料層級資料列計數**indid** = 0 和**indid** = 1，和值會重複**indid** > 1。|  
  
## <a name="remarks"></a>備註  
 不應使用定義為已保留的資料行。  
  
 資料行**dpages**，**保留**，和**用**如果資料表或索引包含 ROW_OVERFLOW 配置單位中的資料，則不會傳回精確的結果。 另外，每個索引的頁面計數也都會個別追蹤，不會彙總基底資料表這些計數。 若要檢視頁面計數，請使用[sys.allocation_units](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)或[sys.partitions](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)目錄檢視，或[sys.dm_db_partition_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md)動態管理檢視。  
  
 在 SQL Server 2000 和舊版中，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 會維護資料列層級的修改計數器。 現在，系統則會在資料行層級維護這些計數器。 因此， **rowmodctr**資料行計算，且會產生在舊版中，結果很相似，但不完全相同的結果。  
  
 如果您使用中的值**rowmodctr**來判斷何時更新統計資料，請考慮下列解決方案：  
  
-   不執行任何動作。 新**rowmodctr**值往往可以協助您判斷何時更新統計資料，因為行為相當接近舊版的結果。  
  
-   不使用 AUTO_UPDATE_STATISTICS。 如需詳細資訊，請參閱[統計資料](../../relational-databases/statistics/statistics.md)。  
  
-   利用時間限制來判斷更新統計資料的時間。 例如，每小時、每日或每週。  
  
-   利用應用程式層級的資訊來判斷更新統計資料的時間。 例如，每次的最大值**識別**超出 10,000 變更資料行，或每次在大量插入作業會執行。  
  
## <a name="see-also"></a>請參閱  
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [將系統資料表對應至系統檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
  
  
