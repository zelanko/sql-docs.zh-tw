---
title: sys.fn_net_changes_&lt;capture_instance&gt; (TRANSACT-SQL) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 4eff2dd82db75bf1dc0114477152cb18b9d715d8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47681746"
---
# <a name="sysfnnetchangesltcaptureinstancegt-transact-sql"></a>sys.fn_net_changes_&lt;capture_instance&gt; & Amp;#40;transact-SQL&AMP;#41;
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包裝函式**changes<** 查詢函數。 sys.sp_cdc_generate_wrapper_function 系統預存程序會產生建立這些函數所需的指令碼。  
  
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
 **Datetime**值，表示要包含在結果集的變更資料表項目範圍的低端點。  
  
 只有 cdc.< 擷取執行個體 > _CT 中的資料列變更資料表中具有相關聯的認可時間完全大於*start_time*都併入結果集中。  
  
 如果為這個引數提供 NULL 的值，查詢範圍的低端點將會對應到擷取執行個體之有效範圍的低端點。  
  
 *end_time*  
 **Datetime**值，表示要包含在結果集的變更資料表項目範圍的高端點。  
  
 這個參數可以採用的兩種意義，根據選擇的值的其中一個@closed_high_end_point時於呼叫 sys.sp_cdc_generate_wrapper_function 來產生建立包裝函式的指令碼：  
  
-   @closed_high_end_point = 1  
  
     只有在 cdc.< 擷取執行個體 > _CT 中的資料列變更中有值的資料表\_ \_$start_lsn 和的對應認可時間小於或等於**start_time**都併入結果集中。  
  
-   @closed_high_end_point = 0  
  
     只有在 cdc.< 擷取執行個體 > _CT 中的資料列變更中有值的資料表\_ \_$start_lsn 和對應認可時間嚴格小於**start_time**都併入結果集中。  
  
 如果為這個引數提供 NULL 的值，查詢範圍的高端點將會對應到擷取執行個體之有效範圍的高端點。  
  
 *< row_filter_option >* :: = {所有 | 所有具有遮罩 | 都可以透過合併}  
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
|\<中的資料行@column_list>|**而有所不同**|中所識別的資料行**column_list** sp_cdc_generate_wrapper_function 時呼叫它來產生建立包裝函式的指令碼的引數。 如果*column_list*為 NULL，所有的追蹤的來源資料行都會出現在結果集。|  
|__CDC_OPERATION|**nvarchar(2)**|指示將資料列套用到目標環境時，需要哪一個作業的作業碼。 作業會有所不同的引數值*row_filter_option*下列呼叫中提供：<br /><br /> *row_filter_option* = 'all'、 'all with mask'<br /><br /> 'D' - 刪除作業<br /><br /> 'I' - 插入作業<br /><br /> 'UN' - 更新作業<br /><br /> *row_filter_option* = 'all with merge'<br /><br /> 'D' - 刪除作業<br /><br /> 'M' - 插入作業或更新作業|  
|\<中的資料行@update_flag_list>|**bit**|藉由將 _uflag 附加到資料行名稱所命名的位元旗標。 旗標才會採用非 null 值時，才*row_filter_option* **= 'all with mask'** 並\__CDC_OPERATION **= 'UN'**。 如果在查詢視窗內修改了對應的資料行，它會設定為 1。 否則為 0。|  
  
## <a name="remarks"></a>備註  
 fn_net_changes_<capture_instance> 函數會當做 cdc.fn_cdc_get_net_changes_<capture_instance> 查詢函數的包裝函數。 sys.sp_cdc_generate_wrapper 預存程序是用來建立此包裝函數的指令碼。  
  
 系統不會自動建立包裝函數。 您必須執行兩項作業，才能建立包裝函數：  
  
1.  執行預存程序來產生用來建立此包裝函數的指令碼。  
  
2.  執行指令碼來實際建立包裝函數。  
  
 包裝函數可讓使用者有系統地查詢所限定之間隔內發生的變更**datetime**值而非 LSN 值。 包裝函式執行之間提供所有必要的轉換**datetime**值和查詢函數的引數作為內部所需的 LSN 值。 循序使用包裝函式來處理變更資料的資料流時, 它們會確定沒有資料遺失或重複是遵循下列慣例： @end_time 為提供與某個呼叫相關聯之間隔的值@start_time與後續呼叫相關聯之間隔的值。  
  
 在建立指令碼時使用 @closed_high_end_point 參數，您便可以產生包裝函式來支援指定之查詢視窗上的封閉上限或開放上限。 也就是說，您可以決定具有認可時間的項目是否等於要包含在間隔內之擷取間隔的上限。 預設會包含上限。  
  
 所傳回的結果集，也就是說**changes<** 包裝函式只有追蹤資料行中的函式會傳回@column_list產生包裝函式時。 如果 @column_list 為 NULL，就會傳回所有追蹤來源資料行。 來源資料行後面緊跟著 __CDC_OPERATION 作業資料行，這是可識別此作業的單字元或雙字元資料行。  
  
 位元旗標則會附加至結果集中的每個資料行中的參數識別@update_flag_list。 針對**changes<** 包裝函式，位元旗標一定會是 NULL，如果@row_filter_option也就是包裝函式呼叫中使用是 'all' all with merge'。 如果@row_filter_option設為 'all with mask'，而且 __CDC_OPERATION 為 ' 或 'I' 旗標的值也會是 NULL。 如果\__CDC_OPERATION 為 ' UN '，此旗標會設定為 1 或 0，這取決於是否**net**更新作業導致資料行的變更。  
  
 「具現化結構描述的 CDC 包裝函數 TVF」異動資料擷取組態範本會示範如何使用 sp_cdc_generate_wrapper_function 預存程序，針對結構描述之已定義查詢函數的所有包裝函數取得 CREATE 指令碼。 然後，此範本會建立這些指令碼。 如需有關範本的詳細資訊，請參閱 <<c0> [ 範本總管](../../ssms/template/template-explorer.md)。  
  
## <a name="see-also"></a>另請參閱  
 [sys.sp_cdc_generate_wrapper_function &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql.md)   
 [cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)  
  
  
