---
title: fn_net_changes_&lt;capture_instance&gt; （transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fn_net_changes_TSQL
- fn_net_changes_TSQL
- fn_net_changes
- sys.fn_net_changes
dev_langs:
- TSQL
helpviewer_keywords:
- fn_net_changes_<capture_instance>
- sys.fn_net_changes_<capture_instance>
ms.assetid: 342fa030-9fd9-4b74-ae4d-49f6038a5073
author: rothja
ms.author: jroth
ms.openlocfilehash: 556518a5fc2950ff69e6a872df5387b4c8367c6b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "68122574"
---
# <a name="sysfn_net_changes_ltcapture_instancegt-transact-sql"></a>sys.databases fn_net_changes_&lt;capture_instance&gt; （transact-sql）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **Net changes**查詢函數的包裝函式。 sys.sp_cdc_generate_wrapper_function 系統預存程序會產生建立這些函數所需的指令碼。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
fn_net_changes_<capture_instance> ('start_time', 'end_time', '<row_filter_option>' )  
  
<capture_instance> ::= The name of the capture instance.  
<row_filter_option> ::=  
{ all  
  | all with mask  
  | all with merge  
}  
```  
  
## <a name="arguments"></a>引數  
 *start_time*  
 **Datetime**值，表示要包含在結果集內之變更資料表專案範圍的低端點。  
  
 只有位於 cdc. <capture_instance>_CT 變更資料表的資料列，且該資料集的關聯認可時間嚴格大於*start_time* ，才會包含在結果集中。  
  
 如果為這個引數提供 NULL 的值，查詢範圍的低端點將會對應到擷取執行個體之有效範圍的低端點。  
  
 *end_time*  
 **Datetime**值，表示要包含在結果集內之變更資料表專案範圍的高階點。  
  
 這個參數可以採用兩個意義的其中一個，這取決於呼叫 sp_cdc_generate_wrapper_function @closed_high_end_point sys.databases 時所選擇的值，以產生建立包裝函式的腳本：  
  
-   @closed_high_end_point = 1  
  
     只有 cdc. <中的資料列會 capture_instance>_CT 變更資料表中具有\_ \_$start _lsn 中的值，而且對應的認可時間小於或等於**start_time**會包含在結果集中。  
  
-   @closed_high_end_point = 0  
  
     只有 cdc. <中的資料列會 capture_instance>_CT 變更資料表具有\_ \_$start _lsn 中的值，而且在結果集中包含嚴格小於**start_time**的對應認可時間。  
  
 如果為這個引數提供 NULL 的值，查詢範圍的高端點將會對應到擷取執行個體之有效範圍的高端點。  
  
 *<row_filter_option>* ：： = {all | all with mask | all with merge}  
 管理結果集中傳回之中繼資料資料行以及資料列內容的選項。 可以是下列其中一個選項：  
  
 all  
 傳回內容資料行內已變更之資料列的最後內容，以及在 __CDC_OPERATION 中繼資料行內套用資料列所需的作業。  
  
 all with mask  
 傳回內容資料行內所有已變更之資料列的最後內容，以及在 __CDC_OPERATION 中繼資料行內套用每一個資料列所需的作業。 如果當您產生用來建立包裝函數的指令碼時，指定了更新旗標清單，則填入更新遮罩需要這個選項。  
  
 all with merge  
 傳回內容資料行內所有已變更之資料列的最後內容。  
  
 __CDC_OPERATION 資料行將會是以下兩個值的其中一個：  
  
-   D (如果必須刪除此資料列的話)。  
  
-   M (如果必須插入或更新此資料列的話)。  
  
 判斷需要插入或更新才能將變更套用至目標的邏輯會增加查詢的複雜性。 不需要區別插入和更新作業時，使用此選項可以改善效能。 在可直接使用合併作業的目標環境 (例如 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 環境) 中，這個方法的效果最好。  
  
## <a name="table-returned"></a>傳回的資料表  
  
|資料行名稱|資料行類型|描述|  
|-----------------|-----------------|-----------------|  
|\<> 的@column_list資料行|**差異**|呼叫以產生建立包裝函式的腳本時，在 sp_cdc_generate_wrapper_function 的**column_list**引數中識別的資料行。 如果*column_list*為 Null，所有追蹤的來源資料行都會出現在結果集中。|  
|__CDC_OPERATION|**nvarchar(2)**|指示將資料列套用到目標環境時，需要哪一個作業的作業碼。 作業會根據下列呼叫中提供的引數*row_filter_option*值而有所不同：<br /><br /> *row_filter_option* = ' all '、' all with mask '<br /><br /> 'D' - 刪除作業<br /><br /> 'I' - 插入作業<br /><br /> 'UN' - 更新作業<br /><br /> *row_filter_option* = ' 全部使用 merge '<br /><br /> 'D' - 刪除作業<br /><br /> 'M' - 插入作業或更新作業|  
|\<> 的@update_flag_list資料行|**bit**|藉由將 _uflag 附加到資料行名稱所命名的位元旗標。 只有當*row_filter_option* **= ' all with mask '** 和\__CDC_OPERATION **= ' UN '** 時，旗標才會採用非 null 值。 如果在查詢視窗內修改了對應的資料行，它會設定為 1。 否則為 0。|  
  
## <a name="remarks"></a>備註  
 Fn_net_changes_<capture_instance> 函式可作為 cdc. fn_cdc_get_net_changes_<capture_instance> 查詢函數的包裝函式。 sys.sp_cdc_generate_wrapper 預存程序是用來建立此包裝函數的指令碼。  
  
 系統不會自動建立包裝函數。 您必須執行兩項作業，才能建立包裝函數：  
  
1.  執行預存程序來產生用來建立此包裝函數的指令碼。  
  
2.  執行指令碼來實際建立包裝函數。  
  
 包裝函式可讓使用者有系統地查詢在以**datetime**值（而不是 LSN 值）限制的間隔內發生的變更。 包裝函式會在提供的**datetime**值與內部所需的 LSN 值之間執行所有必要的轉換，做為查詢函數的引數。 當包裝函式使用順序來處理變更資料的資料流程時，它們會確保不會遺失或重復資料，但前提是遵循下列慣例：與一個@end_time呼叫相關聯的間隔值會當做與後續呼叫相關@start_time聯之間隔的值提供。  
  
 在建立指令碼時使用 @closed_high_end_point 參數，您便可以產生包裝函式來支援指定之查詢視窗上的封閉上限或開放上限。 也就是說，您可以決定具有認可時間的項目是否等於要包含在間隔內之擷取間隔的上限。 預設會包含上限。  
  
 **Net changes**包裝函數所傳回的結果集，只會傳回產生包裝函式時，在中@column_list的追蹤資料行。 如果 @column_list 為 NULL，就會傳回所有追蹤來源資料行。 來源資料行後面緊跟著 __CDC_OPERATION 作業資料行，這是可識別此作業的單字元或雙字元資料行。  
  
 然後，在參數@update_flag_list中識別的每個資料行的結果集上附加位旗標。 對於**淨變更**包裝函式，如果在包裝函式的呼叫中@row_filter_option使用的是「全部」或「全部使用 merge」，位旗標一定會是 Null。 @row_filter_option如果設定為 ' all with mask '，且 __CDC_OPERATION 為 ' d ' 或 ' I '，則旗標的值也會是 Null。 如果\__CDC_OPERATION 為「取消」，則會將旗標設為1或0，這取決於**net** update 作業是否會導致資料行變更。  
  
 「變更資料捕獲設定範本」具現化架構的 CDC 包裝函式 Tvf 說明如何使用 sp_cdc_generate_wrapper_function 預存程式，針對架構定義的查詢函式的所有包裝函式取得建立腳本。 然後，此範本會建立這些指令碼。 如需範本的詳細資訊，請參閱[範本瀏覽器](../../ssms/template/template-explorer.md)。  
  
## <a name="see-also"></a>另請參閱  
 [sp_cdc_generate_wrapper_function &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql.md)   
 [cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)  
  
  
