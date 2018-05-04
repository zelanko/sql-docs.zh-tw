---
title: sp_estimate_data_compression_savings (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_estimate_data_compression_savings_TSQL
- sp_estimate_data_compression_savings
dev_langs:
- TSQL
helpviewer_keywords:
- compression [SQL Server], estimating
- sp_estimate_data_compression_savings
ms.assetid: 6f6c7150-e788-45e0-9d08-d6c2f4a33729
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 533e4245bc731b55eeb373aa86fd10947d84488c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="spestimatedatacompressionsavings-transact-sql"></a>sp_estimate_data_compression_savings (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回要求之物件目前的大小，並針對要求的壓縮狀態預估物件大小。 可以針對整個資料表或部分資料表評估壓縮， 這包括堆積、叢集索引、非叢集索引、索引檢視表以及資料表和索引資料分割。 您可以使用資料列壓縮或頁面壓縮來壓縮物件。 如果資料表、索引或資料分割已經壓縮，您可以使用此程序來估計已重新壓縮之資料表、索引或資料分割的大小。  
  
> [!NOTE]  
>  壓縮和**sp_estimate_data_compression_savings**不是每個版本都可使用[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本支援的功能清單，請參閱 [SQL Server 2016 版本支援的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
 若要預估使用要求壓縮設定之物件的大小，此預存程序會取樣來源物件，並將此資料載入 tempdb 內所建立的同等資料表和索引中。 然後會將 tempdb 內所建立的資料表或索引壓縮成要求的設定，並計算預估的壓縮節省程度。  
  
 若要變更資料表、 索引或資料分割，使用的壓縮狀態[ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)或[ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md)陳述式。 如需壓縮的一般資訊，請參閱[資料壓縮](../../relational-databases/data-compression/data-compression.md)。  
  
> [!NOTE]  
>  如果現有的資料已分割，您或許能夠減少資料的大小，而不需要重建索引來使用壓縮。 如果是索引，將會在索引重建時套用填滿因數， 這樣可能會增加索引的大小。  

 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_estimate_data_compression_savings   
     [ @schema_name = ] 'schema_name'    
   , [ @object_name = ] 'object_name'   
   , [@index_id = ] index_id   
   , [@partition_number = ] partition_number   
   , [@data_compression = ] 'data_compression'   
[;]  
```  
  
## <a name="arguments"></a>引數  
 [ @schema_name=] '*schema_name*'  
 這是包含資料表或索引檢視表的資料庫結構描述名稱。 *schema_name*是**sysname**。 如果*schema_name*為 NULL，就會使用目前使用者的預設結構描述。  
  
 [ @object_name=] '*object_name*'  
 這是索引所在的資料表或索引檢視表名稱。 *object_name* 是 **sysname**.  
  
 [ @index_id=] '*index_id*'  
 這是索引的識別碼。 *index_id*是**int**，而且可以是下列值之一： 索引、 NULL 或 0 的 ID 編號*object_id*是堆積。 若要傳回基底資料表或檢視表的所有索引相關資訊，請指定 NULL。 如果您指定 NULL，您也必須指定為 NULL 。  
  
 [ @partition_number=] ''  
 這是物件的分割區編號。 是**int**，而且可以是下列值之一： 索引或堆積、 NULL 或非資料分割索引或堆積的 1 的分割區編號。  
  
 若要指定資料分割，您也可以指定[$partition](../../t-sql/functions/partition-transact-sql.md)函式。 若要傳回主控物件之所有資料分割的相關資訊，請指定 NULL。  
  
 [ @data_compression=] '*data_compression*'  
 這是要評估的壓縮類型。 *data_compression*可以是下列值之一： NONE、 ROW 或 PAGE。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 系統會傳回下列結果集，以提供目前和估計之資料表、索引或資料分割的大小。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|object_name|**sysname**|資料表或索引檢視表的名稱。|  
|schema_name|**sysname**|資料表或索引檢視表的結構描述。|  
|index_id|**int**|索引的索引識別碼：<br /><br /> 0 = 堆積<br /><br /> 1 = 叢集索引<br /><br /> > 1 = 非叢集索引|  
|partition_number|**int**|資料分割編號。 如果是非資料分割的資料表或索引，則會傳回 1。|  
|size_with_current_compression_setting (KB)|**bigint**|目前存在且要求之資料表、索引或資料分割的大小。|  
|size_with_requested_compression_setting (KB)|**bigint**|使用要求之壓縮設定的資料表、索引或資料分割的估計大小，以及適用的現有填滿因數 (假設沒有片段)。|  
|sample_size_with_current_compression_setting (KB)|**bigint**|包含目前壓縮設定之樣本的大小。 其中包含所有片段。|  
|sample_size_with_requested_compression_setting (KB)|**bigint**|使用要求之壓縮設定所建立的樣本大小，以及適用的現有填滿因數 (沒有片段)。|  
  
## <a name="remarks"></a>備註  
 使用 sp_estimate_data_compression_savings 可估計當您啟用資料表或資料分割進行資料列或頁面壓縮時，可以產生的節省程度。 例如，如果資料列的平均大小可縮減 40%，您就可能會將物件的大小縮減 40%。 您可能無法節省空間，因為這是根據填滿因數和資料列的大小而定。 例如，如果您有一個長度為 8000 個位元組的資料列，而且您將它的大小縮減 40%，則仍然只能在資料頁面上容納單一資料列。 無法節省任何空間。  
  
 如果執行 sp_estimate_data_compression_savings 的結果指示資料表將會成長，就表示資料表中的許多資料列都使用資料類型的幾乎完整有效位數，而且壓縮格式所需的小型負擔增加會比壓縮的空間節省更大。 在這種罕見情況下，請勿啟用壓縮。  
  
 如果資料表已啟用壓縮，請使用 sp_estimate_data_compression_savings 來估計未壓縮資料表時的資料列平均大小。  
  
 進行這項作業期間，將會取得資料表的 (IS) 鎖定。 如果無法取得 (IS) 鎖定，此程序將會遭到封鎖。 資料表會在讀取認可的隔離等級下掃描。  
  
 如果要求的壓縮設定與目前的壓縮設定相同，則預存程序將會傳回估計的大小，其中不含任何資料片段，而且會使用現有的填滿因數。  
  
 如果此索引或資料分割識別碼不存在，則不會傳回任何結果。  
  
## <a name="permissions"></a>Permissions  
 需要資料表的 SELECT 權限。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
 此程序不適用於資料行存放區資料表，因此不接受 COLUMNSTORE 和 COLUMNSTORE_ARCHIVE 資料壓縮參數。  
  
## <a name="examples"></a>範例  
 下列範例會估計 `Production.WorkOrderRouting` 資料表的大小 (如果使用 `ROW` 壓縮來將它壓縮)。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_estimate_data_compression_savings 'Production', 'WorkOrderRouting', NULL, NULL, 'ROW' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [sys.partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [Database Engine 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Unicode 壓縮實作](../../relational-databases/data-compression/unicode-compression-implementation.md)  
  
  
