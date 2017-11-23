---
title: "ALTER WORKLOAD GROUP (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2016
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_WORKLOAD_GROUP_TSQL
- ALTER WORKLOAD GROUP
dev_langs: TSQL
helpviewer_keywords: ALTER WORKLOAD GROUP statement
ms.assetid: 957addce-feb0-4e54-893e-5faca3cd184c
caps.latest.revision: "56"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7bfb6ca0200095860acec2b275020012e4b96284
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="alter-workload-group-transact-sql"></a>ALTER WORKLOAD GROUP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  變更現有的資源管理員工作負載群組組態，並選擇性地將其指派給資源管理員資源集區。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [TRANSACT-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
ALTER WORKLOAD GROUP { group_name | "default" }  
[ WITH  
    ([ IMPORTANCE = { LOW | MEDIUM | HIGH } ]  
      [ [ , ] REQUEST_MAX_MEMORY_GRANT_PERCENT = value ]  
      [ [ , ] REQUEST_MAX_CPU_TIME_SEC = value ]  
      [ [ , ] REQUEST_MEMORY_GRANT_TIMEOUT_SEC = value ]   
      [ [ , ] MAX_DOP = value ]  
      [ [ , ] GROUP_MAX_REQUESTS = value ] )  
 ]  
[ USING { pool_name | "default" } ]  
[ ; ]  
```  
  
## <a name="arguments"></a>引數  
 *group_name* |「**預設**"  
 這是現有使用者定義之工作負載群組的名稱，或是資源管理員預設工作負載群組的名稱。  
  
> [!NOTE]  
>  當您安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，資源管理員就會建立此 "default" 和內部群組。  
  
 搭配 ALTER WORKLOAD GROUP 使用時，"default" 選項必須加上引號 ("") 或方括號 ([]) 才能避免與系統保留字 DEFAULT 產生衝突。 如需詳細資訊，請參閱＜ [Database Identifiers](../../relational-databases/databases/database-identifiers.md)＞。  
  
> [!NOTE]  
>  預先定義的工作負載群組和資源集區都會使用小寫名稱，例如 "default"。 如果是使用區分大小寫之定序的伺服器，則應該將此列入考量。 具有不區分大小寫之定序 (如 SQL_Latin1_General_CP1_CI_AS) 的伺服器會將 "default" 和 "Default" 視為相同。  
  
 IMPORTANCE = { LOW | MEDIUM | HIGH }  
 指定要求在工作負載群組中的相對重要性。 重要性為下列其中一項：  
  
-   LOW  
  
-   MEDIUM (預設值)  
  
-   HIGH  
  
> [!NOTE]  
>  每個重要性設定在內部都會儲存為計算所使用的數字。  
  
 IMPORTANCE 的資源集區範圍為本機；相同資源集區內部不同重要性的工作負載群組會彼此影響，但不會影響另一個資源集區中的工作負載群組。  
  
 REQUEST_MAX_MEMORY_GRANT_PERCENT =*值*  
 指定單一要求可由集區中獲取的記憶體最大數量。 這個百分比相對於 MAX_MEMORY_PERCENT 所指定的資源集區大小。  
  
> [!NOTE]  
>  指定的數量僅參考查詢執行授與記憶體。  
  
 *值*必須是 0 或正整數。 允許的範圍*值*是從 0 到 100。 預設設定*值*為 25。  
  
 請注意下列事項：  
  
-   設定*值*設為 0 可防止具有使用者定義的工作負載群組中的 SORT 和 HASH JOIN 作業的查詢執行。  
  
-   我們不建議您設定*值*大於 70 因為伺服器可能無法安排足夠的可用記憶體，如果在其他並行查詢正在執行。 最後，這可能會導致查詢逾時錯誤 8645。  
  
> [!NOTE]  
>  如果查詢記憶體需求超過這個參數所指定的限制，伺服器會執行以下作業：  
>   
>  如果是使用者定義的工作負載群組，伺服器會嘗試減少查詢的平行處理原則程度，直到記憶體需求低於此限制，或是直到平行處理原則程度等於 1 為止。 如果查詢記憶體需求仍然大於此限制，將會發生錯誤 8657。  
>   
>  如果是內部和預設的工作負載群組，伺服器會允許查詢取得所需的記憶體。  
>   
>  請注意，如果伺服器沒有足夠的實體記憶體，這兩種情況都會受限於逾時錯誤 8645。  
  
 REQUEST_MAX_CPU_TIME_SEC =*值*  
 指定要求可以使用的最大 CPU 時間量 (以秒為單位)。 *值*必須是 0 或正整數。 預設設定*值*為 0，表示無限制。  
  
> [!NOTE]  
>  資源管理員不會在超過最大時間時阻止要求繼續執行。 不過，系統將會產生某個事件。 如需詳細資訊，請參閱[CPU Threshold Exceeded Event Class<](../../relational-databases/event-classes/cpu-threshold-exceeded-event-class.md)。  
  
 REQUEST_MEMORY_GRANT_TIMEOUT_SEC =*值*  
 指定查詢能夠等待記憶體授權 (工作緩衝區記憶體) 變成可用的最大時間 (以秒為單位)。  
  
> [!NOTE]  
>  到達記憶體授權的逾時值時，查詢不一定會失敗。 只有當有太多並行的查詢正在執行時，查詢才會失敗。 否則，查詢可能只會得到最小的記憶體授權，導致查詢效能降低。  
  
 *值*必須是正整數。 預設設定*值*，0，會使用內部計算根據查詢成本來決定最大時間。  
  
 MAX_DOP =*值*  
 為平行要求指定平行處理原則的最大程度 (DOP)。 *值*必須是 0 或正整數，1 到 255。 當*值*是 0，則伺服器會選擇平行處理原則的最大程度。 這是預設值且為建議的設定。  
  
> [!NOTE]  
>  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 針對 MAX_DOP 所設定的實際值可能會小於指定的值。 最終的值由公式 min (255， *Cpu 的數目)*。  
  
> [!CAUTION]  
>  變更 MAX_DOP 可能會對伺服器的效能造成不良影響。 如果您必須變更 MAX_DOP，我們建議您將它設定為小於或等於存在單一 NUMA 節點中之最大硬體排程器數目的值。 我們建議您不要將 MAX_DOP 設定為大於 8 的值。  
  
 MAX_DOP 會以下列方式處理：  
  
-   只要 MAX_DOP 沒有超過工作負載群組 MAX_DOP，就會接受當做查詢提示的 MAX_DOP。  
  
-   當做查詢提示的 MAX_DOP 永遠會覆寫 sp_configure 的「平行處理原則的最大程度」。  
  
-   工作負載群組 MAX_DOP 會覆寫 sp_configure 的「平行處理原則的最大程度」。  
  
-   如果查詢在編譯時間被標示為序列 (MAX_DOP = 1)，不管工作負載群組或 sp_configure 設定為何，都無法在執行階段將該查詢變更回平行。  
  
 DOP 經過設定後，在授與記憶體不足的壓力下，僅能將其降低。 在授與記憶體佇列中等候時，看不到工作負載群組的重新組態。  
  
 GROUP_MAX_REQUESTS =*值*  
 指定在工作負載群組中可允許執行的最大同時要求數。 *值*必須是 0 或正整數。 預設設定*值*，0，允許無限制的要求。 達到最大並行要求時，該群組中的使用者可以登入，但是會處於等候狀態，直到並行要求低於指定的值為止。  
  
 使用 { *pool_name* |「**預設**"}  
 將工作負載群組與所識別的使用者定義的資源集區相關聯*pool_name*，實際上將工作負載群組放入資源集區。 如果*pool_name*未提供或未使用 USING 引數，如果工作負載群組會放入預先定義的資源管理員預設集區。  
  
 搭配 ALTER WORKLOAD GROUP 使用時，"default" 選項必須加上引號 ("") 或方括號 ([]) 才能避免與系統保留字 DEFAULT 產生衝突。 如需詳細資訊，請參閱＜ [Database Identifiers](../../relational-databases/databases/database-identifiers.md)＞。  
  
> [!NOTE]  
>  "default" 選項會區分大小寫。  
  
## <a name="remarks"></a>備註  
 在預設群組中允許使用 ALTER WORKLOAD GROUP。  
  
 工作負載群組組態的變更在執行 ALTER RESOURCE GOVERNOR RECONFIGURE 前不會生效。 當變更會影響設定的計劃，新設定才會生效先前快取計劃中執行 DBCC FREEPROCCACHE 之後 (*pool_name*)，其中*pool_name*是資源的名稱管理員工作負載群組是與相關聯的資源集區。  
  
-   如果您要變更 max_dop 會固定為 1，執行 DBCC FREEPROCCACHE 不需要因為平行計畫能以序列模式執行。 不過，它可能無法編譯為以序列計畫的計畫的效率。  
  
-   如果您從 1 變更 max_dop 會固定為 0 或大於 1，執行 DBCC FREEPROCCACHE 不需要。 不過，序列計畫無法以平行方式執行，所以清除個別的快取將會允許新計劃可能會進行編譯使用平行處理原則。  
  
> [!CAUTION]  
>  清除快取的計畫，從一個以上的工作負載群組相關聯的資源集區將會影響所有工作負載群組與使用者定義的資源集區識別*pool_name*。  
  
 當您要執行 DDL 陳述式時，建議您先熟悉資源管理員的狀態。 如需詳細資訊，請參閱[Resource Governor](../../relational-databases/resource-governor/resource-governor.md)。  
  
 REQUEST_MEMORY_GRANT_PERCENT：在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中，允許建立索引即可使用比一開始授與之記憶體更多的工作空間記憶體來改善效能。 資源管理員的更新版本中支援此特殊處理，不過，初始授與和任何額外的記憶體授與都會受到資源集區和工作負載群組設定的限制。  
  
 **資料分割資料表上建立索引**  
  
 非對齊式分割區資料表上之索引建立所耗用的記憶體，與相關的分割區數目成正比。  如果所需的總記憶體超出資源管理員工作負載群組設定所設的每個查詢限制 (REQUEST_MAX_MEMORY_GRANT_PERCENT)，這個索引建立動作就可能無法執行。 由於 "default" 工作負載群組允許查詢超過每個查詢限制，而且具有 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 相容性啟動所需的記憶體下限，因此使用者或許能夠在 "default" 工作負載群組中執行相同的索引建立動作，但前提是 "default" 資源集區有設定足夠的總記憶體來執行這類查詢。  
  
## <a name="permissions"></a>Permissions  
 需要 CONTROL SERVER 權限。  
  
## <a name="examples"></a>範例  
 下列範例顯示如何將預設群組中的要求重要性從 `MEDIUM` 變更為 `LOW`。  
  
```  
ALTER WORKLOAD GROUP "default"  
WITH (IMPORTANCE = LOW);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
 下列範例顯示如何將工作負載群組從所屬集區移到預設集區。  
  
```  
ALTER WORKLOAD GROUP adHoc  
USING [default];  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>請參閱＜  
 [資源管理員](../../relational-databases/resource-governor/resource-governor.md)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)   
 [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)   
 [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  
