---
title: cdc.fn_cdc_get_net_changes_&lt;capture_instance&gt; (TRANSACT-SQL) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 8d60f772d7848d0e207f83b5c7a1a10da4b43b37
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47804936"
---
# <a name="cdcfncdcgetnetchangesltcaptureinstancegt-transact-sql"></a>cdc.fn_cdc_get_net_changes_&lt;capture_instance&gt; & Amp;#40;transact-SQL&AMP;#41;
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回指定的記錄順序編號 (LSN) 範圍內變更每個來源資料列傳回一個淨變更的資料列。  
  
 **等一下，LSN 是什麼？** 在每一筆記錄[SQL Server 交易記錄檔](../logs/the-transaction-log-sql-server.md)會識別記錄序號 (LSN)。 LSNs 經過排序，因此如果 LSN2 大於 LSN1，LSN2 所參考的記錄檔記錄所發生**之後**記錄 lsn1 所描述的變更。  
  
 發生重大事件記錄檔記錄的 LSN，可用於建構正確的還原順序。 因為 LSNs 經過排序，您可以比較它們是否相等和不等比較 (亦即\<，>、 =、 \<=、 > =)。 要建構還原順序時，這種比較很有用。  
  
 當來源資料列會有多項變更的 LSN 範圍內時，如下所述的列舉型別函式會傳回單一資料列，以反映資料列的最終內容。 例如，如果交易的來源資料表中插入一個資料列之 LSN 範圍內的後續交易更新該資料列中的一或多個資料行，此函式只會傳回**一個**資料列，其中包括更新的資料行值。  
  
 當來源資料表啟用變更資料擷取並指定了淨追蹤時，就會建立此列舉函數。 若要啟用淨追蹤，來源資料表必須具有主索引鍵或唯一的索引。 函數名稱衍生自並採用格式 cdc.fn_cdc_get_net_changes_*capture_instance*，其中*capture_instance*是來源資料表時，指定擷取執行個體的值啟用異動資料擷取。 如需詳細資訊，請參閱 < [sys.sp_cdc_enable_table &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)。  
  
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
 LSN，代表要包含在結果集之 LSN 範圍的低端點。 *from_lsn*已**binary(10)**。  
  
 只有當資料列中[cdc。&#91;擷取執行個體&#93;_CT](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md)變更資料表的值大於或等於 __ $start_lsn *from_lsn*都併入結果集中。  
  
 *to_lsn*  
 LSN，代表要包含在結果集之 LSN 範圍的高端點。 *to_lsn*已**binary(10)**。  
  
 只有當資料列中[cdc。&#91;擷取執行個體&#93;_CT](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md)變更資料表的值 __ $start_lsn 中小於或等於*from_lsn*或等於*to_lsn*會包含在結果集中。  
  
 *< row_filter_option >* :: = {所有 | 所有具有遮罩 | 都可以透過合併}  
 管理結果集中傳回之中繼資料資料行以及資料列內容的選項。 可以是下列其中一個選項：  
  
 all  
 傳回的資料列和套用中繼資料行 __ $start_lsn 中的資料列所需的作業的最終變更的 LSN 以及\_ \_$operation。 資料行\_ \_$update_mask 一律為 NULL。  
  
 all with mask  
 傳回的資料列和套用中繼資料行 __ $start_lsn 中的資料列所需的作業的最終變更的 LSN 以及\_ \_$operation。 此外，當更新作業傳回 (\_\_$operation = 4) 中傳回的值中標示更新中修改的擷取資料行\_ \_$update_mask。  
  
 all with merge  
 在中繼資料資料行 __$start_lsn 中傳回資料列最終變更的 LSN。 資料行\_ \_$operation 會是兩個值之一： 1 代表刪除，而 5 則表示套用變更所需的作業是插入或更新。 資料行\_ \_$update_mask 一律為 NULL。  
  
 由於針對指定變更判斷精確作業的邏輯會增加查詢的複雜性，所以這個選項會設計成在足以表示套用變更所需的作業是插入或更新時改善查詢效能，但是不一定要明確區分這兩者。 在可直接使用合併作業的目標環境 (例如 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 環境) 中，這個選項最具吸引力。  
  
## <a name="table-returned"></a>傳回的資料表  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|__$start_lsn|**binary(10)**|與變更之認可交易相關聯的 LSN。<br /><br /> 在相同交易中認可的所有變更都會共用相同的認可 LSN。 例如，如果來源資料表上的更新作業修改了兩個資料列中的兩個資料行，變更資料表將會包含四個資料列，每個都具有相同的 __ $start_lsnvalue。|  
|__$operation|**int**|識別將變更資料的資料列套用至目標資料來源所需的資料操作語言 (DML) 作業。<br /><br /> 如果 row_filter_option 參數的值為 all 或 all with mask，則此資料行中的值可能為下列其中一個值：<br /><br /> 1 = 刪除<br /><br /> 2 = 插入<br /><br /> 4 = 更新<br /><br /> 如果 row_filter_option 參數的值為 all with merge，則此資料行中的值可能為下列其中一個值：<br /><br /> 1 = 刪除|  
|__$update_mask|**varbinary(128)**|位元遮罩，其中含有對應至針對擷取執行個體所識別之每個擷取資料行的位元。 當 __$operation = 1 或 2 時，這個值會將所有定義的位元都設定為 1。 當\_ \_$operation = 3 或 4，只有變更的資料行的對應位元才會設定為 1。|  
|*\<擷取的來源資料表資料行>*|變化|這個函數所傳回的其餘資料行都是建立擷取執行個體時，在來源資料表中識別成擷取資料行的資料行。 如果擷取的資料行清單中沒有指定任何資料行，就會傳回來源資料表中的所有資料行。|  
  
## <a name="permissions"></a>Permissions  
 需要系統管理員 (sysadmin) 固定伺服器角色或 db_owner 固定資料庫角色中的成員資格。 若為所有其他使用者，則需要來源資料表中所有擷取資料行的 SELECT 權限，而且如果定義了擷取執行個體的控制角色，便需要該資料庫角色的成員資格。 當呼叫端沒有檢視來源資料的權限時，此函數就會傳回錯誤 208 (無效的物件名稱)。  
  
## <a name="remarks"></a>備註  
 如果指定的 LSN 範圍不在擷取執行個體的變更追蹤時間表內，此函數就會傳回錯誤 208 (無效的物件名稱)。

 資料列上的唯一識別項修改會導致 fn_cdc_get_net_changes 來顯示初始的更新命令，以刪除，並改為插入惡意軟體移除命令。  此行為是為了同時變更之前和之後，追蹤索引鍵。
  
## <a name="examples"></a>範例  
 下列範例會使用函式`cdc.fn_cdc_get_net_changes_HR_Department`報告對來源資料表所做的淨變更`HumanResources.Department`在特定時間間隔內。  
  
 首先，`GETDATE` 函數是用來標示時間間隔的開頭。 在許多 DML 陳述式都套用至來源資料表之後，系統就會再次呼叫 `GETDATE` 函數來識別時間間隔的結尾。 此函式[sys.fn_cdc_map_time_to_lsn](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md)然後用來將時間間隔對應至 LSN 值所限定變更資料擷取查詢範圍。 最後，系統會查詢 `cdc.fn_cdc_get_net_changes_HR_Department` 函數，以便針對時間間隔取得來源資料表的淨變更。 請注意，先插入後刪除的資料列不會顯示在此函數所傳回的結果集中。 這是因為在查詢視窗中先加入後刪除的資料列不會在該間隔內於來源資料表上產生任何淨變更。 執行此範例之前，您必須先執行中的範例 B [sys.sp_cdc_enable_table &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)。  
  
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
 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)   
 [sys.fn_cdc_map_time_to_lsn &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md)   
 [sys.sp_cdc_enable_table &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)   
 [sys.sp_cdc_help_change_data_capture &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)   
 [關於異動資料擷取 &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
  
