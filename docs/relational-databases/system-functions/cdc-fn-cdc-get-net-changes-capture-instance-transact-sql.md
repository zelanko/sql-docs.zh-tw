---
title: cdc. fn_cdc_get_net_changes_&lt;capture_instance&gt; （transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- fn_cdc_get_net_changes_<capture_instance>
- change data capture [SQL Server], querying metadata
- cdc.fn_cdc_get_net_changes_<capture_instance>
ms.assetid: 43ab0d1b-ead4-471c-85f3-f6c4b9372aab
author: rothja
ms.author: jroth
ms.openlocfilehash: 77fb03c71bd0773cc8f004a89c28c1925284876b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68043040"
---
# <a name="cdcfn_cdc_get_net_changes_ltcapture_instancegt-transact-sql"></a>cdc. fn_cdc_get_net_changes_&lt;capture_instance&gt; （transact-sql）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對在指定的記錄序號（LSN）範圍內變更的每個來源資料列，各傳回一個淨變更資料列。  
  
 **等待，什麼是 LSN？** [SQL Server 事務](../logs/the-transaction-log-sql-server.md)歷史記錄中的每個記錄都是以記錄序號（LSN）來唯一識別。 Lsn 的排序方式是，如果 LSN2 大於 LSN1，則 LSN2 所參考的記錄檔記錄所描述的變更會在記錄檔記錄 LSN 所描述的變更**之後**發生。  
  
 發生重大事件之記錄檔記錄的 LSN，可能有助於用來建立正確的還原順序。 因為 Lsn 經過排序，所以您可以比較它們是否相等和不相等（也\<就是，>， \<=，=，>=）。 要建構還原順序時，這種比較很有用。  
  
 當來源資料列在 LSN 範圍內有多個變更時，列舉函數會傳回一個反映資料列最終內容的單一資料列，如下所述。 例如，如果交易在來源資料表中插入資料列，而 LSN 範圍內的後續交易更新該資料列中的一個或多個資料行，則此函數只會傳回**一個**資料列，其中包含更新的資料行值。  
  
 當來源資料表啟用變更資料擷取並指定了淨追蹤時，就會建立此列舉函數。 若要啟用淨追蹤，來源資料表必須具有主索引鍵或唯一的索引。 函式名稱是衍生的，而且會使用 fn_cdc_get_net_changes_*capture_instance*的格式，其中*capture_instance*是當來源資料表啟用變更資料捕獲時，針對 capture 實例所指定的值。 如需詳細資訊，請參閱[sp_cdc_enable_table &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
cdc.fn_cdc_get_net_changes_capture_instance ( from_lsn , to_lsn , '<row_filter_option>' )  
  
<row_filter_option> ::=  
{ all  
 | all with mask  
 | all with merge  
}  
```  
  
## <a name="arguments"></a>引數  
 *from_lsn*  
 LSN，代表要包含在結果集之 LSN 範圍的低端點。 *from_lsn*為**binary （10）**。  
  
 只有在[cdc. &#91;](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md)中的資料列 capture_instance&#93;_CT 變更資料表的值在 __ $ start_lsn 大於或等於*from_lsn*中，才會包含在結果集中。  
  
 *to_lsn*  
 LSN，代表要包含在結果集之 LSN 範圍的高端點。 *to_lsn*為**binary （10）**。  
  
 只有[cdc. &#91;](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md)中的資料列會 capture_instance&#93;_CT 變更資料表，其中的值在 __ $ start_lsn 小於或等於*from_lsn*或等於*to_lsn*會包含在結果集中。  
  
 *<row_filter_option>* ：： = {all | all with mask | all with merge}  
 管理結果集中傳回之中繼資料資料行以及資料列內容的選項。 可以是下列其中一個選項：  
  
 所有  
 傳回資料列最後一項變更的 LSN，以及套用中繼資料行 __ $ start_lsn 和\_ \_$operation 所需的作業。 資料行\_ \_$update 的 _mask 一律為 Null。  
  
 all with mask  
 傳回資料列最後一項變更的 LSN，以及套用中繼資料行 __ $ start_lsn 和\_ \_$operation 所需的作業。 此外，當更新作業\_\_傳回（$operation = 4）時，在更新中修改的已捕捉資料行會在\_ \_$update _mask 中傳回的值中標示。  
  
 all with merge  
 在中繼資料資料行 __$start_lsn 中傳回資料列最終變更的 LSN。 $Operation 的\_ \_資料行是兩個值的其中一個：1代表刪除，而5則表示套用變更所需的作業是插入或更新。 資料行\_ \_$update 的 _mask 一律為 Null。  
  
 由於針對指定變更判斷精確作業的邏輯會增加查詢的複雜性，所以這個選項會設計成在足以表示套用變更所需的作業是插入或更新時改善查詢效能，但是不一定要明確區分這兩者。 在可直接使用合併作業的目標環境 (例如 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 環境) 中，這個選項最具吸引力。  
  
## <a name="table-returned"></a>傳回的資料表  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|__$start_lsn|**binary （10）**|與變更之認可交易相關聯的 LSN。<br /><br /> 在相同交易中認可的所有變更都會共用相同的認可 LSN。 例如，如果來源資料表上的更新作業修改了兩個數據列中的兩個數據行，則變更資料表會包含四個數據列，每個資料列都有相同的 __ $ start_lsnvalue。|  
|__$operation|**int**|識別將變更資料的資料列套用至目標資料來源所需的資料操作語言 (DML) 作業。<br /><br /> 如果 row_filter_option 參數的值為 all 或 all with mask，則此資料行中的值可能為下列其中一個值：<br /><br /> 1 = 刪除<br /><br /> 2 = 插入<br /><br /> 4 = 更新<br /><br /> 如果 row_filter_option 參數的值為 all with merge，則此資料行中的值可能為下列其中一個值：<br /><br /> 1 = 刪除|  
|__$update_mask|**Varbinary （128）**|位元遮罩，其中含有對應至針對擷取執行個體所識別之每個擷取資料行的位元。 當 __$operation = 1 或 2 時，這個值會將所有定義的位元都設定為 1。 當\_ \_$operation = 3 或4時，只有對應至已變更之資料行的位會設定為1。|  
|*\<已捕獲的來源資料表資料行>*|視情況而異|這個函數所傳回的其餘資料行都是建立擷取執行個體時，在來源資料表中識別成擷取資料行的資料行。 如果擷取的資料行清單中沒有指定任何資料行，就會傳回來源資料表中的所有資料行。|  
  
## <a name="permissions"></a>權限  
 需要系統管理員 (sysadmin) 固定伺服器角色或 db_owner 固定資料庫角色中的成員資格。 若為所有其他使用者，則需要來源資料表中所有擷取資料行的 SELECT 權限，而且如果定義了擷取執行個體的控制角色，便需要該資料庫角色的成員資格。 當呼叫端沒有檢視來源資料的權限時，此函數就會傳回錯誤 208 (無效的物件名稱)。  
  
## <a name="remarks"></a>備註  
 如果指定的 LSN 範圍不在擷取執行個體的變更追蹤時間表內，此函數就會傳回錯誤 208 (無效的物件名稱)。

 修改資料列的唯一識別碼，會導致 fn_cdc_get_net_changes 使用 DELETE 和 INSERT 命令來顯示初始的 UPDATE 命令。  這是在變更前後追蹤金鑰所需的行為。
  
## <a name="examples"></a>範例  
 下列範例會使用函數`cdc.fn_cdc_get_net_changes_HR_Department`來報告在特定時間間隔內對來源資料表`HumanResources.Department`所做的淨變更。  
  
 首先，`GETDATE` 函數是用來標示時間間隔的開頭。 在許多 DML 陳述式都套用至來源資料表之後，系統就會再次呼叫 `GETDATE` 函數來識別時間間隔的結尾。 然後，會使用[fn_cdc_map_time_to_lsn](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md)函數將時間間隔對應至由 lsn 值所系結的變更資料捕獲查詢範圍。 最後，系統會查詢 `cdc.fn_cdc_get_net_changes_HR_Department` 函數，以便針對時間間隔取得來源資料表的淨變更。 請注意，先插入後刪除的資料列不會顯示在此函數所傳回的結果集中。 這是因為在查詢視窗中先加入後刪除的資料列不會在該間隔內於來源資料表上產生任何淨變更。 執行此範例之前，您必須先在 sys.databases 中執行範例 B [sp_cdc_enable_table &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @begin_time datetime, @end_time datetime, @from_lsn binary(10), @to_lsn binary(10);  
-- Obtain the beginning of the time interval.  
SET @begin_time = GETDATE() -1;  
-- DML statements to produce changes in the HumanResources.Department table.  
INSERT INTO HumanResources.Department (Name, GroupName)  
VALUES (N'MyDept', N'MyNewGroup');  
  
UPDATE HumanResources.Department  
SET GroupName = N'Resource Control'  
WHERE GroupName = N'Inventory Management';  
  
DELETE FROM HumanResources.Department  
WHERE Name = N'MyDept';  
  
-- Obtain the end of the time interval.  
SET @end_time = GETDATE();  
-- Map the time interval to a change data capture query range.  
SET @from_lsn = sys.fn_cdc_map_time_to_lsn('smallest greater than or equal', @begin_time);  
SET @to_lsn = sys.fn_cdc_map_time_to_lsn('largest less than or equal', @end_time);  
  
-- Return the net changes occurring within the query window.  
SELECT * FROM cdc.fn_cdc_get_net_changes_HR_Department(@from_lsn, @to_lsn, 'all');  
```  
  
## <a name="see-also"></a>另請參閱  
 [cdc. fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-sql&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)   
 [fn_cdc_map_time_to_lsn &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md)   
 [sp_cdc_enable_table &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)   
 [sp_cdc_help_change_data_capture &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)   
 [關於異動資料擷取 &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
  
