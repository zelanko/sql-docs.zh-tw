---
title: "cdc。&lt;capture_instance&gt;_CT (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 05/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- cdc
- cdc_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.<capture_instance>_CT
ms.assetid: 979c8110-3c54-4e76-953c-777194bc9751
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 53f2078f3894d5db7c398b2470b4a3625320e948
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="cdcltcaptureinstancegtct-transact-sql"></a>cdc。&lt;capture_instance&gt;_CT (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  這是在來源資料表啟用異動資料擷取時所建立的變更資料表。 此資料表會針對在來源資料表上執行的每個插入和刪除作業傳回一個資料列，而且會針對在來源資料表上執行的每個更新作業傳回兩個資料列。 如果在啟用來源資料表時沒有指定變更資料表的名稱，就會衍生此名稱。 名稱的格式為 cdc。*capture_instance*_CT 其中*capture_instance*是來源資料表的結構描述名稱和來源資料表中的名稱格式*schema_table*。 例如，如果資料表**Person.Address**中**AdventureWorks**範例資料庫啟用了異動資料擷取，衍生的變更資料表名稱就是**cdc。Person_Address_CT**。  
  
 我們建議您**不直接查詢系統資料表**。 請改為執行[cdc.fn_cdc_get_all_changes_ < capture_instance >](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)和[cdc.fn_cdc_get_net_changes_ < capture_instance >](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)函式。  
  

  
|資料行名稱|資料類型|說明|  
|-----------------|---------------|-----------------|  
|**__$start_lsn**|**binary(10)**|與變更之認可交易相關聯的記錄序號 (LSN)。<br /><br /> 在相同交易中認可的所有變更都會共用相同的認可 LSN。 例如，如果來源資料表上的刪除作業會移除兩個資料列，變更資料表將會包含兩個資料列，每個具有相同**__ $start_lsn**值。|  
|**__ $ end_lsn**|**binary(10)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> 在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中，這個資料行一律是 NULL。|  
|**__$seqval**|**binary(10)**|用來排序交易內資料列變更的序列值。|  
|**__$operation**|**int**|識別與變更相關聯的資料操作語言 (DML) 作業。 可以是下列其中一項：<br /><br /> 1 = 刪除<br /><br /> 2 = 插入<br /><br /> 3 = 更新 (舊的值)<br /><br /> 執行更新陳述式之前，資料行資料具有資料列值。<br /><br /> 4 = 更新 (新的值)<br /><br /> 執行更新陳述式之後，資料行資料具有資料列值。|  
|**__$update_mask**|**varbinary(128)**|位元遮罩，可根據變更資料表的資料行序數識別這些變更的資料行。|  
|*\<擷取來源資料表資料行 >*|變化|變更資料表中的其餘資料行都是建立擷取執行個體時，在來源資料表中識別成擷取資料行的資料行。 如果擷取的資料行清單中沒有指定任何資料行，這個資料表就會包含來源資料表中的所有資料行。|  
|**__ $ command_id** |**int** |會追蹤在交易內的作業的順序。 |  
  
## <a name="remarks"></a>備註  

`__$command_id`資料行的資料行在累計更新版本到 2016/2012年中引進。 版本和下載資訊，請參閱知識庫文章 3030352 在[修正： 變更資料表排序不正確地更新資料列之後啟用異動資料擷取的 Microsoft SQL Server 資料庫](https://support.microsoft.com/help/3030352/fix-the-change-table-is-ordered-incorrectly-for-updated-rows-after-you)。  如需詳細資訊，請參閱[CDC 功能可能會中斷之後升級至最新 CU for SQL Server 2012、 2014年到 2016年](https://blogs.msdn.microsoft.com/sql_server_team/cdc-functionality-may-break-after-upgrading-to-the-latest-cu-for-sql-server-2012-2014-and-2016/)。

## <a name="captured-column-data-types"></a>擷取資料行資料類型  
 包含在這個資料表中的擷取資料行與對應的來源資料行具有相同的資料類型和值，但下列情況除外：  
  
-   **時間戳記**資料行定義為**binary （8)**。  
  
-   **識別**資料行定義為**int**或**bigint**。  
  
 不過，這些資料行中的值與來源資料行的值相同。  
  
### <a name="large-object-data-types"></a>大型物件資料類型  
 資料類型的資料行**映像**，**文字**，和**ntext**一律指派**NULL**值 __ $operation = 1 或\_\_$operation = 3。 資料類型的資料行**varbinary （max)**， **varchar （max)**，或**nvarchar （max)**指派**NULL**值時\_\_$operation = 3，除非資料行在更新期間變更。 當\_ \_$operation = 1，這些資料行會在刪除時指定其值。 一律包含在擷取執行個體中的計算資料行的值為**NULL**。  
  
 根據預設，在單一 INSERT、UPDATE、WRITETEXT 或 UPDATETEXT 陳述式中可加入至擷取資料行的大小上限為 65,536 個位元組或 64 KB。 若要增加這個大小以便支援更大的 LOB 資料，請使用[設定 max text repl size 伺服器組態選項](../../database-engine/configure-windows/configure-the-max-text-repl-size-server-configuration-option.md)來指定較大的大小上限。 如需詳細資訊，請參閱 [設定 max text repl size 伺服器組態選項](../../database-engine/configure-windows/configure-the-max-text-repl-size-server-configuration-option.md)。  
  
## <a name="data-definition-language-modifications"></a>資料定義語言修改  
 來源資料表中，例如加入或卸除資料行的 DDL 修改會記錄在[cdc.ddl_history](../../relational-databases/system-tables/cdc-ddl-history-transact-sql.md)資料表。 這些變更不會套用至變更資料表。 也就是說，變更資料表的定義會維持不變。 將資料列插入變更資料表時，擷取處理序會忽略沒有顯示在與來源資料表相關聯之擷取資料行清單中的這些資料行。 如果某個資料行顯示在擷取資料行清單中，但是該資料行已不存在來源資料表中，系統就會指派 Null 值給此資料行。  
  
 變更來源資料表中的資料行的資料類型也會記錄於[cdc.ddl_history](../../relational-databases/system-tables/cdc-ddl-history-transact-sql.md)資料表。 不過，這項變更不會更改變更資料表的定義。 當擷取處理序遇到對來源資料表所做 DDL 變更的記錄檔記錄時，變更資料表中擷取資料行的資料類型就會遭修改。  
  
 如果您必須以減少資料類型大小的方式來修改來源資料表中擷取資料行的資料類型，請使用下列程序來確保變更資料表中的對等資料行可成功進行修改。  
  
1.  在來源資料表中，更新即將修改之資料行的值，以便符合規劃的資料類型大小。 例如，如果您變更資料類型，從**int**至**smallint**，這些值更新為在需要調整大小**smallint**範圍-32,768 到 32,767。  
  
2.  在變更資料表中，在對等的資料行上執行相同的更新作業。  
  
3.  透過指定新的資料類型，更改來源資料表。 然後，資料類型變更就會成功地傳播至變更資料表。  
  
## <a name="data-manipulation-language-modifications"></a>資料操作語言修改  
 在啟用異動資料擷取的來源資料表上執行插入、更新和刪除作業時，這些 DML 作業的記錄就會顯示在資料庫交易記錄中。 異動資料擷取的擷取處理序會從交易記錄中擷取這些變更的相關資訊，然後將一或兩個資料列加入至變更資料表，以便記錄變更。 雖然變更資料表項目的認可通常必須針對一組變更而非單一項目執行，不過將項目加入至變更資料表的順序會與來源資料表認可這些項目的順序相同。  
  
 變更資料表項目內**__ $start_lsn**資料行用來記錄的認可 LSN 所關聯的來源資料表變更，而**__ $seqval 資料行**用來排序內變更其交易。 這些中繼資料資料行可一起用來確保來源變更的認可順序會保留下來。 由於擷取處理序會從交易記錄中取得其變更資訊，因此請務必注意，變更資料表項目不會以同步方式隨著其對應的來源資料表變更顯示。 不過，當擷取處理序已經處理來自交易記錄的相關變更項目之後，對應的變更會以非同步方式顯示。  
  
 若為插入和刪除作業，就會設定更新遮罩中的所有位元。 若為更新作業，就會同時修改更新舊值與更新新值資料列中的更新遮罩，以便反映在更新期間變更的資料行。  
  
## <a name="see-also"></a>請參閱＜  
 [sys.sp_cdc_enable_table &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)   
 [sys.sp_cdc_get_ddl_history &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-ddl-history-transact-sql.md)  
  
  
