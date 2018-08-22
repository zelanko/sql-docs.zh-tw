---
title: sys.fn_all_changes_&lt;capture_instance&gt; (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server (starting with 2008)
f1_keywords:
- fn_all_changes
- sys.fn_all_changes
- fn_all_changes_TSQL
- sys.fn_all_changes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_all_changes_<capture_instance>
- sys.fn_all_changes_<capture_instance>
ms.assetid: 564fae96-b88c-4f22-9338-26ec168ba6f5
caps.latest.revision: 15
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f9e6be682816d4a7572414d9e91d0840cc6417aa
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/16/2018
ms.locfileid: "40394017"
---
# <a name="sysfnallchangesltcaptureinstancegt-transact-sql"></a>sys.fn_all_changes_&lt;capture_instance&gt; & Amp;#40;transact-SQL&AMP;#41;
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包裝函式**的所有變更**查詢函數。 sys.sp_cdc_generate_wrapper_function 系統預存程序會產生建立這些函數所需的指令碼。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
fn_all_changes_<capture_instance> ('start_time' ,'end_time', '<row_filter_option>' )  
  
<capture_instance> ::= The name of the capture instance.  
<row_filter_option> ::=  
{ all  
  | all update old  
}  
```  
  
## <a name="arguments"></a>引數  
 *start_time*  
 **Datetime**值，表示要包含在結果集的變更資料表項目範圍的低端點。  
  
 只有在 cdc.< 擷取執行個體 > _CT 中的資料列變更資料表中具有相關聯的認可時間大於*start_time*都併入結果集中。  
  
 如果為這個引數提供 NULL 的值，查詢範圍的低端點將會對應到擷取執行個體之有效範圍的低端點。  
  
 *end_time*  
 **Datetime**值，表示要包含在結果集的變更資料表項目範圍的高端點。  
  
 這個參數可以採用的兩個可能的意思，根據選擇的值的其中一個@closed_high_end_point時於呼叫 sys.sp_cdc_generate_wrapper_function 來產生包裝函式的建立指令碼：  
  
-   @closed_high_end_point = 1  
  
     結果集只包含 cdc.<capture_instance>_CT 變更資料表內的資料列，這些資料列的相關聯認可時間小於或等於 end_time。  
  
-   @closed_high_end_point = 0  
  
     結果集只包含 cdc.capture_instance_CT 變更資料表內的資料列，這些資料列的相關聯認可時間嚴格小於 end_time。  
  
 如果為這個引數提供 NULL 的值，查詢範圍的高端點將會對應到擷取執行個體之有效範圍的高端點。  
  
 <row_filter_option> ::= { all | all update old }  
 管理結果集中傳回之中繼資料資料行及資料列內容的選項。  
  
 可以是下列其中一個選項：  
  
 all  
 傳回指定之 LSN 範圍內的所有變更。 如果是因為更新作業所發生的變更，這個選項就只會傳回包含套用更新之後之新值的資料列。  
  
 all update old  
 傳回指定之 LSN 範圍內的所有變更。 如果是因為更新作業而發生的變更，這個選項就會同時傳回包含更新之前之資料行值的資料列以及包含更新之後之資料行值的資料列。  
  
## <a name="table-returned"></a>傳回的資料表  
  
|資料行名稱|資料行類型|描述|  
|-----------------|-----------------|-----------------|  
|__CDC_STARTLSN|**binary(10)**|與變更相關聯之交易的認可 LSN。 在相同交易中認可的所有變更都會共用相同的認可 LSN。|  
|__CDC_SEQVAL|**binary(10)**|用來排序交易內資料列變更的序列值。|  
|\<中的資料行@column_list>|**而有所不同**|中所識別的資料行*column_list* sp_cdc_generate_wrapper_function 時呼叫它來產生建立包裝函式的指令碼的引數。|  
|__CDC_OPERATION|**nvarchar(2)**|表示將資料列套用到目標環境所需之作業的作業碼。 它會因引數的值*row_filter_option*呼叫中提供：<br /><br /> *row_filter_option* = 'all'<br /><br /> 'D' - 刪除作業<br /><br /> 'I' - 插入作業<br /><br /> 'UN' - 更新作業新值<br /><br /> *row_filter_option* = 'all update old'<br /><br /> 'D' - 刪除作業<br /><br /> 'I' - 插入作業<br /><br /> 'UN' - 更新作業新值<br /><br /> 'UO' - 更新作業舊值|  
|\<中的資料行@update_flag_list>|**bit**|藉由將 _uflag 附加到資料行名稱所命名的位元旗標。 旗標一定會設定為 NULL 時\__CDC_OPERATION 為 '，'I'，'或 'uo'。 當\__CDC_OPERATION 為 ' UN '，如果更新產生了對應資料行的變更，它會設定為 1。 否則為 0。|  
  
## <a name="remarks"></a>備註  
 fn_all_changes_<capture_instance> 函數會當做 cdc.fn_cdc_get_all_changes_<capture_instance> 查詢函數的包裝函數。 sys.sp_cdc_generate_wrapper 預存程序是用來產生建立此包裝函數的指令碼。  
  
 系統不會自動建立包裝函數。 您必須執行兩項作業，才能建立包裝函數：  
  
1.  執行預存程序來產生用來建立此包裝函數的指令碼。  
  
2.  執行指令碼來實際建立包裝函數。  
  
 包裝函數可讓使用者有系統地查詢所限定之間隔內發生的變更**datetime**值而非 LSN 值。 包裝函式執行之間提供所有必要的轉換**datetime**值和查詢函數的引數作為內部所需的 LSN 值。 循序使用包裝函式來處理變更資料的資料流時, 它們會確定沒有資料遺失或重複是遵循下列慣例： @end_time 為提供與某個呼叫相關聯之間隔的值@start_time與後續呼叫相關聯之間隔的值。  
  
 在建立指令碼時使用 @closed_high_end_point 參數，您便可以產生包裝函式來支援指定之查詢視窗上的封閉上限或開放上限。 也就是說，您可以決定具有認可時間的項目是否等於要包含在間隔內之擷取間隔的上限。 預設會包含上限。  
  
 所傳回的結果集，也就是說**的所有變更**包裝函式的函式會傳回 __ $start_lsn 和\_ \_$seqval 資料表資料行變更為資料行\__CDC_STARTLSN 和\__CDC_SEQVAL，分別。 它只追蹤的資料行出現在具有會跟*@column_list*時所產生的包裝函式的參數。 如果*@column_list*為 NULL，就會傳回資料行的所有追蹤來源。 來源資料行後面接著作業資料行， \__CDC_OPERATION，它是一個或兩個字元資料行可識別此作業。  
  
 然後，系統會針對 @update_flag_list 參數內識別的每個資料行，將位元旗標附加到結果集。 針對**的所有變更**包裝函式，位元旗標一定會是 NULL 如果 __CDC_OPERATION 為有 '，'I' 或 'UO'。 如果\__CDC_OPERATION 為 ' UN '，旗標會設為 1 或 0，這取決於更新作業是否會導致資料行的變更。  
  
 「具現化結構描述的 CDC 包裝函數 TVF」異動資料擷取組態範本會示範如何使用 sp_cdc_generate_wrapper_function 預存程序，針對結構描述之已定義查詢函數的所有包裝函數取得 CREATE 指令碼。 然後，此範本會建立這些指令碼。 如需有關範本的詳細資訊，請參閱 <<c0> [ 範本總管](../../ssms/template/template-explorer.md)。  
  
## <a name="see-also"></a>另請參閱  
 [sys.sp_cdc_generate_wrapper_function &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql.md)   
 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)  
  
  
