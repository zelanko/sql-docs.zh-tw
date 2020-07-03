---
title: sp_estimate_data_compression_savings （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 08/26/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 94eeb0baeae20327650d0291e0ca4f1725abb1d9
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85881735"
---
# <a name="sp_estimate_data_compression_savings-transact-sql"></a>sp_estimate_data_compression_savings (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  傳回要求之物件目前的大小，並針對要求的壓縮狀態預估物件大小。 可以針對整個資料表或部分資料表評估壓縮， 這包括堆積、叢集索引、非叢集索引、資料行存放區索引、索引視圖，以及資料表和索引資料分割。 您可以使用資料列、頁面、資料行存放區或資料行存放區封存壓縮來壓縮物件。 如果資料表、索引或資料分割已經壓縮，您可以使用此程序來估計已重新壓縮之資料表、索引或資料分割的大小。  
  
> [!NOTE]
> 並非所有版本都可使用壓縮和**sp_estimate_data_compression_savings** [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本支援的功能清單，請參閱 [SQL Server 2016 版本支援的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
 若要預估使用要求壓縮設定之物件的大小，此預存程序會取樣來源物件，並將此資料載入 tempdb 內所建立的同等資料表和索引中。 然後會將 tempdb 內所建立的資料表或索引壓縮成要求的設定，並計算預估的壓縮節省程度。  
  
 若要變更資料表、索引或資料分割的壓縮狀態，請使用[ALTER table](../../t-sql/statements/alter-table-transact-sql.md)或[alter index](../../t-sql/statements/alter-index-transact-sql.md)語句。 如需有關壓縮的一般資訊，請參閱[資料壓縮](../../relational-databases/data-compression/data-compression.md)。  
  
> [!NOTE]  
> 如果現有的資料已分割，您或許能夠減少資料的大小，而不需要重建索引來使用壓縮。 如果是索引，將會在索引重建時套用填滿因數， 這樣可能會增加索引的大小。  

 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
sp_estimate_data_compression_savings   
     [ @schema_name = ] 'schema_name'    
   , [ @object_name = ] 'object_name'   
   , [ @index_id = ] index_id   
   , [ @partition_number = ] partition_number   
   , [ @data_compression = ] 'data_compression'   
[;]  
```  
  
## <a name="arguments"></a>引數  
 [ @schema_name =] '*schema_name*'  
 這是包含資料表或索引檢視表的資料庫結構描述名稱。 *schema_name*是**sysname**。 如果*schema_name*為 Null，則會使用目前使用者的預設架構。  
  
 [ @object_name =] '*object_name*'  
 這是索引所在的資料表或索引檢視表名稱。 *object_name* 是 **sysname**.  
  
 [ @index_id =] *index_id*  
 這是索引的識別碼。 *index_id*是**int**，而且可以是下列其中一個值：索引的識別碼、Null 或0（如果*object_id*是堆積）。 若要傳回基底資料表或檢視表的所有索引相關資訊，請指定 NULL。 如果您指定 Null，則也必須為*partition_number*指定 null。  
  
 [ @partition_number =] *partition_number*  
 這是物件的分割區編號。 *partition_number*是**int**，而且可以是下列其中一個值：索引或堆積的資料分割編號、Null 或1（代表非資料分割索引或堆積）。  
  
 若要指定分割區，您也可以指定[$partition](../../t-sql/functions/partition-transact-sql.md)函數。 若要傳回主控物件之所有資料分割的相關資訊，請指定 NULL。  
  
 [ @data_compression =] '*data_compression*'  
 這是要評估的壓縮類型。 *data_compression*可以是下列其中一個值： NONE、ROW、PAGE、資料行存放區或 COLUMNSTORE_ARCHIVE。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 系統會傳回下列結果集，以提供目前和估計之資料表、索引或資料分割的大小。  
  
|資料行名稱|資料類型|描述|  
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
 用 `sp_estimate_data_compression_savings` 來估計當您啟用資料列、頁面、資料行存放區或資料行存放區封存壓縮的資料表或資料分割時，可能會發生的節約。 例如，如果資料列的平均大小可縮減 40%，您就可能會將物件的大小縮減 40%。 您可能無法節省空間，因為這是根據填滿因數和資料列的大小而定。 例如，如果您有一個長度為8000個位元組的資料列，而您將其大小縮減為40%，則您仍然只能在資料頁面上容納一個資料列。 無法節省任何空間。  
  
 如果執行 `sp_estimate_data_compression_savings` 的結果指示資料表將會成長，就表示資料表中的許多資料列都使用資料類型的幾乎完整有效位數，而且壓縮格式所需的小型負擔增加會比壓縮的空間節省更大。 在這種罕見情況下，請勿啟用壓縮。  
  
 如果資料表已啟用壓縮，請使用 `sp_estimate_data_compression_savings` 來估計未壓縮資料表時的資料列平均大小。  
  
 進行這項作業期間，將會取得資料表的 (IS) 鎖定。 如果無法取得 (IS) 鎖定，此程序將會遭到封鎖。 資料表會在讀取認可的隔離等級下掃描。  
  
 如果要求的壓縮設定與目前的壓縮設定相同，則預存程序將會傳回估計的大小，其中不含任何資料片段，而且會使用現有的填滿因數。  
  
 如果此索引或資料分割識別碼不存在，則不會傳回任何結果。  
  
## <a name="permissions"></a>權限  
 必須具備資料表的`SELECT`權限。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
 在 SQL Server 2019 之前，這個程式不會套用至資料行存放區索引，因此不接受資料壓縮參數資料行存放區和 COLUMNSTORE_ARCHIVE。  從 SQL Server 2019 開始，資料行存放區索引可以用來做為估計的來源物件，以及做為要求的壓縮類型。

 > [!IMPORTANT]
 > 在中啟用[記憶體優化 TempDB 中繼資料](../databases/tempdb-database.md#memory-optimized-tempdb-metadata)時 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] ，不支援在臨時表上建立資料行存放區索引。 基於這項限制，當已啟用記憶體優化的 TempDB 中繼資料時，資料行存放區和 COLUMNSTORE_ARCHIVE 資料壓縮參數不支援 sp_estimate_data_compression_savings。

## <a name="considerations-for-columnstore-indexes"></a>資料行存放區索引的考量
 從開始 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] ，支援同時評估資料行存放區和資料行存放區封存 `sp_estimate_compression_savings` 壓縮。 不同于頁面和資料列壓縮，對物件套用資料行存放區壓縮時，需要建立新的資料行存放區索引。 因此，在使用此程式的資料行存放區和 COLUMNSTORE_ARCHIVE 選項時，提供給程式的來源物件類型會決定用於壓縮大小估計的資料行存放區索引類型。 下表說明當參數設定為 [資料行存放區] 或 [COLUMNSTORE_ARCHIVE] 時，用來估計每個來源物件類型之壓縮節省量的參考物件 @data_compression 。

 |來源物件|參考物件|
 |-----------------|---------------|
 |堆積|叢集資料行存放區索引|
 |叢集索引|叢集資料行存放區索引|
 |非叢集索引|非叢集資料行存放區索引（包括所提供非叢集索引的索引鍵資料行和任何內含資料行），以及資料表的資料分割資料行（如果有的話）|
 |非叢集資料行存放區索引|非叢集資料行存放區索引（包含與所提供非叢集資料行存放區索引相同的資料行|
 |叢集資料行存放區索引|叢集資料行存放區索引|

> [!NOTE]  
> 當您從 rowstore 來源物件（叢集索引、非叢集索引或堆積）評估資料行存放區壓縮時，如果來源物件中的任何資料行具有資料行存放區索引不支援的資料類型，sp_estimate_compression_savings 將會失敗並產生錯誤。

 同樣地，當 `@data_compression` 參數設定為 `NONE` 、 `ROW` 或，而來源物件為數據行存放區索引時 `PAGE` ，下表會列出所使用的參考物件。

 |來源物件|參考物件|
 |-----------------|---------------|
 |叢集資料行存放區索引|堆積|
 |非叢集資料行存放區索引|非叢集索引（包括包含在非叢集資料行存放區索引中做為索引鍵資料行的資料行），以及資料表的分割區資料行（如果有的話）做為內含資料行）|

> [!NOTE]  
> 從資料行存放區來源物件中評估 rowstore 壓縮（NONE、ROW 或 PAGE）時，請確定來源索引未包含超過32個數據行，因為這是 rowstore （非叢集）索引中支援的限制。
  
## <a name="examples"></a>範例  
 下列範例會估計 `Production.WorkOrderRouting` 資料表的大小 (如果使用 `ROW` 壓縮來將它壓縮)。  
  
```sql  
USE AdventureWorks2016;  
GO  
EXEC sp_estimate_data_compression_savings 'Production', 'WorkOrderRouting', NULL, NULL, 'ROW' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [sys.databases &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [資料庫引擎預存程式 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Unicode 壓縮實作](../../relational-databases/data-compression/unicode-compression-implementation.md)  
  
  
