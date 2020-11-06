---
description: dm_execution_performance_counters (SSISDB 資料庫)
title: dm_execution_performance_counters (SSISDB 資料庫) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 1b38e8e3-c560-4b6e-b60e-bfd7cfcd4fdf
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 19111422e69b2ce77f53e13bb6d1a450b4ef7692
ms.sourcegitcommit: 80701484b8f404316d934ad2a85fd773e26ca30c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93243664"
---
# <a name="functions---dm_execution_performance_counters"></a>函式 - dm_execution_performance_counters

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]

  傳回 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 伺服器上執行之執行的效能統計資料。  
  
## <a name="syntax"></a>語法  
  
```sql  
dm_execution_performance_counters [ @execution_id = ] execution_id  
  
```  
  
## <a name="arguments"></a>引數  
 [ @execution_id = ] *execution_id*  
 包含一個或多個封裝之執行的唯一識別碼。 以「執行封裝」工作執行的封裝，會與父封裝在相同執行中執行。  
  
 如果沒有指定的執行識別碼，則會傳回多個執行的效能統計資料。 如果您是 **ssis_admin** 資料庫角色的成員，則會傳回所有執行中之執行的效能統計資料。  如果您不是 **ssis_admin** 資料庫角色的成員，則會傳回您具有讀取權限之執行中執行的效能統計資料。 *execution_id* 是 **BigInt** 。  
  
## <a name="remarks"></a>備註  
 下表列出 dm_execution_performance_counter 函數傳回的計數器名稱值。  
  
|計數器名稱|描述|  
|------------------|-----------------|  
|BLOB bytes read|資料流程引擎從所有來源讀取之二進位大型物件 (BLOB) 資料的位元組數目。|  
|BLOB bytes written|資料流程引擎寫入至所有目的地的 BLOB 資料位元組數目。|  
|BLOB files in use|資料流程引擎用於多工緩衝處理的 BLOB 檔案數目。|  
|Buffer memory|Integration Services 緩衝區所使用的記憶體數量，包括實體和虛擬記憶體。|  
|Buffers in use|所有資料流程元件及資料流程引擎正在使用之所有類型的緩衝區物件數目。|  
|Buffers Spooled|寫入磁碟的緩衝區數目。|  
|Flat buffer memory|所有一般緩衝區使用的記憶體數目 (以位元組為單位)。 一般緩衝區是元件用以儲存資料的記憶體區塊。|  
|Flat buffers in use|資料流程引擎所使用的一般緩衝區數目。 所有一般緩衝區都是私用緩衝區。|  
|Private buffer memory|所有私用緩衝區使用中的記憶體數目。 私用緩衝區是轉換用於暫存工作的緩衝區。<br /><br /> 如果資料流程引擎建立緩衝區來支援資料流程，該緩衝區就不是私用緩衝區。|  
|Private buffers in use|轉換用於暫存工作的緩衝區數目。|  
|Rows read|執行讀取的資料列總數。|  
|Rows written|執行寫入的資料列總數。|  
  
## <a name="return"></a>傳回  
 dm_execution_performance_counters 函數會針對執行中的執行，傳回含有下列資料行的資料表。 傳回的資訊適用於執行中包含的所有封裝。 如果沒有執行中的執行，就會傳回空的資料表。  
  
|資料行名稱|資料行類型|描述|備註|  
|-----------------|-----------------|-----------------|-------------|  
|execution_id|**BigInt**<br /><br /> **NULL** 是無效的值。|包含封裝之執行的唯一識別碼。||  
|counter_name|**nvarchar(128)**|計數器的名稱。|請參閱值的 **備註** 一節。|  
|counter_value|**BigInt**|計數器傳回的值。||  
  
## <a name="examples"></a>範例  

### <a name="a-return-statistics-for-a-running-execution"></a>A. 傳回執行中執行作業的統計資料

 在下列範例中，函數會傳回識別碼為 34 之執行中執行作業的統計資料。  
  
```sql
select * from [catalog].[dm_execution_performance_counters] (34)  
```  
  
### <a name="b-return-statistics-for-all-running-executions"></a>B. 傳回所有執行中執行作業的統計資料

 在下列範例中，函數會依據您的權限傳回 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 伺服器上執行之所有執行作業的統計資料。  
  
```sql
select * from [catalog].[dm_execution_performance_counters] (NULL)  
  
```  
  
## <a name="permissions"></a>權限  
 這個函數需要下列其中一個權限：  
  
-   執行的執行個體之 READ 和 MODIFY 權限  
  
-   **ssis_admin** 資料庫角色的成員資格  
  
-   **系統管理員** 伺服器角色的成員資格  
  
## <a name="errors-and-warnings"></a>錯誤和警告  
 下列清單描述會導致函數失敗的情況。  
  
-   使用者沒有指定執行的 MODIFY 權限。  
  
-   指定的執行識別碼無效。  
  
  
