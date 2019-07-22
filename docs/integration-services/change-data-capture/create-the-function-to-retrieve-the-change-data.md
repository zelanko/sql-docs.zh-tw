---
title: 建立函數以擷取變更資料 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- incremental load [Integration Services],creating function
ms.assetid: 55dd0946-bd67-4490-9971-12dfb5b9de94
author: janinezhang
ms.author: janinez
ms.openlocfilehash: e4da506162bc50e4089c0077b4b2e94854282c3b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68060829"
---
# <a name="create-the-function-to-retrieve-the-change-data"></a>建立函數以擷取變更資料

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  完成執行累加式變更資料載入之 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝的控制流程後，下一個工作是建立可擷取變更資料的資料表值函式。 第一次累加式載入前，您僅需要建立一次這個函數。  
  
> [!NOTE]  
>  建立可擷取變更資料的函數是建立執行累加式變更資料載入之封裝程序的第二個步驟。 如需建立此封裝之完整程序的描述，請參閱[變更資料擷取 &#40;SSIS&#41;](../../integration-services/change-data-capture/change-data-capture-ssis.md)。  
  
## <a name="design-considerations-for-change-data-capture-functions"></a>異動資料擷取函數的設計考量  
 若要擷取變更資料，封裝之資料流程中的來源元件會呼叫下列其中一個異動資料擷取查詢函數：  
  
-   **cdc.fn_cdc_get_net_changes_<capture_instance>** 對此查詢，會針對每個更新傳回單一資料列，其中包含每個變更資料列的最終狀態。 在大部分的情況下，及僅需要淨變更查詢所傳回的資料。 如需詳細資訊，請參閱 [cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)。  
  
-   **cdc.fn_cdc_get_all_changes_<capture_instance>** 此查詢會傳回擷取間隔期間，在每個資料列中發生的所有變更。 如需詳細資訊，請參閱 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)。  
  
 接著，來源元件會接收函數所傳回的結果，並將這些結果傳遞到下游的轉換和目的地，以便將變更資料套用到最終的目的地。  
  
 不過， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 來源元件無法直接呼叫這些異動資料擷取函數。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 來源元件需要查詢所傳回之資料行的相關中繼資料。 異動資料擷取函數不會定義其輸出資料表的資料行。 因此，這些函數不會針對 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 來源元件傳回足夠的中繼資料。  
  
 但是，由於資料表值包裝函數會在其 RETURNS 子句中，明確定義其輸出資料表的資料行，因此您可以使用此種函數。 此資料行的明確定義會提供 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 來源元件所需的中繼資料。 您必須針對每個您要擷取其變更資料的資料表，建立這個函數。  
  
 您有兩個選擇，可以建立呼叫異動資料擷取查詢函數的資料表值包裝函數：  
  
-   您可以呼叫 **sys.sp_cdc_generate_wrapper_function** 系統預存程序來建立資料表值函式。  
  
-   您可以使用本主題中的指導方針與範例，撰寫自己的資料表值函式。  
  
## <a name="calling-a-stored-procedure-to-create-the-table-valued-function"></a>呼叫預存程序來建立資料表值函式  
 建立您需要之資料表值函式最快速而且簡單的方式，就是呼叫 **sys.sp_cdc_generate_wrapper_function** 系統預存程序。 此預存程序會產生指令碼來建立特別設計的包裝函式，以符合 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 來源元件的需求。  
  
> [!IMPORTANT]  
>  **sys.sp_cdc_generate_wrapper_function** 系統預存程序不會直接建立包裝函式。 但是，預存程序會針對包裝函數產生 CREATE 指令碼。 開發人員必須先執行預存程序所產生的 CREATE 指令碼，累加式載入封裝才能呼叫包裝函數。  
  
 若要了解如何使用此系統預存程序，您應該先了解程序的用途、程序所產生的指令碼，以及指令碼所建立的包裝函數。  
  
### <a name="understanding-and-using-the-stored-procedure"></a>了解與使用預存程序  
 **sys.sp_cdc_generate_wrapper_function** 系統預存程序會產生指令碼來建立 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝使用的包裝函式。  
  
 此處為預存程序定義的前幾行：  
  
 `CREATE PROCEDURE sys.sp_cdc_generate_wrapper_function`  
  
 `(`  
  
 `@capture_instance sysname = null`  
  
 `@closed_high_end_point bit = 1,`  
  
 `@column_list = null,`  
  
 `@update_flag_list = null`  
  
 `)`  
  
 預存程序的所有參數都是選擇性的。 如果您在不提供任何參數值的情況下呼叫預存程序，預存程序就會為您可存取的所有擷取執行個體建立包裝函數。  
  
> [!NOTE]  
>  如需此預存程序之語法及其參數的詳細資訊，請參閱 [sys.sp_cdc_generate_wrapper_function &#40;Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql.md)。  
  
 預存程序永遠會產生一個包裝函數來傳回每個擷取執行個體的所有變更。 如果 *@supports_net_changes* 參數在建立擷取執行個體時設定，預存程序也會產生一個包裝函式來傳回每個適用之擷取執行個體的淨變更。  
  
 預存程序會傳回包含兩個資料行的結果集：  
  
-   預存程序產生之包裝函數的名稱。 此預存程序會從擷取執行個體的名稱衍生函數名稱 (函數名稱為 'fn_all_changes_'，後面接著擷取執行個體名稱。 用於淨變更函數 (如果有建立) 的前置詞為 'fn_net_changes_')。  
  
-   適用於包裝函數的 CREATE 陳述式  
  
### <a name="understanding-and-using-the-scripts-created-by-the-stored-procedure"></a>了解與使用預存程序所建立的指令碼  
 開發人員通常會使用 INSERT...EXEC 陳述式來呼叫 **sys.sp_cdc_generate_wrapper_function** 預存程序，並將預存程序所建立的指令碼儲存到暫存資料表中。 接著，您可以個別選取並執行每個指令碼，以建立對應的包裝函數。 不過，開發人員也可以使用一組 SQL 命令來執行所有 CREATE 指令碼，如下列範例程式碼所示：  
  
```  
create table #wrapper_functions  
      (function_name sysname, create_stmt nvarchar(max))  
insert into #wrapper_functions  
exec sys.sp_cdc_generate_wrapper_function  
  
declare @stmt nvarchar(max)  
declare #hfunctions cursor local fast_forward for   
      select create_stmt from #wrapper_functions  
open #hfunctions  
fetch #hfunctions into @stmt  
while (@@fetch_status <> -1)  
begin  
      exec sp_executesql @stmt  
      fetch #hfunctions into @stmt  
end  
close #hfunctions  
deallocate #hfunctions  
```  
  
### <a name="understanding-and-using-the-functions-created-by-the-stored-procedure"></a>了解與使用預存程序所建立的函數  
 若要有系統地查核已擷取之異動資料的時間表，所產生的包裝函式會預期適用於一個間隔的 *@end_time* 參數將會是適用於後續間隔的 *@start_time* 參數。 遵循此慣例時，所產生的包裝函數可以進行下列工作：  
  
-   將日期/時間值對應到內部使用的 LSN 值。  
  
-   請確定沒有資料遺失或重複。  
  
 為讓變更資料表之所有資料列的查詢更為簡單，所產生的包裝函數也支援下列慣例：  
  
-   如果 @start_time 參數為 Null，包裝函數會使用擷取執行個體中最低的 LSN 值，作為查詢的下限。  
  
-   如果 @end_time 參數為 Null，包裝函數會使用擷取執行個體中最高的 LSN 值，作為查詢的上限。  
  
 大部分使用者應該都可以在不修改的情況下，使用 **sys.sp_cdc_generate_wrapper_function** 系統預存程序所建立的包裝函式。 不過，若要自訂包裝函數，您必須先自訂 CREATE 指令碼，然後再執行這些指令碼。  
  
 當您的封裝呼叫包裝函數時，該封裝必須提供三個參數的值。 這三個參數就像異動資料擷取函數所使用的三個參數。 這三個參數如下所示：  
  
-   間隔的開始日期/時間值和結束日期/時間值。 當包裝函數使用日期/時間值做為查詢間隔的端點時，異動資料擷取函數會使用兩個 LSN 值做為端點。  
  
-   資料列篩選器。 對於包裝函式與異動資料擷取函數而言， *@row_filter_option* 參數相同。 如需詳細資訊，請參閱 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md) 和 [cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)。  
  
 包裝函數所傳回的結果集包含下列資料：  
  
-   異動資料的所有要求資料行。  
  
-   名稱為 __CDC_OPERATION 的資料行使用一或兩個字元欄位來識別與資料列關聯的作業。 此欄位的有效值如下：'I' 用於插入、'D' 用於刪除、'UO'’ 用於更新舊值，而 'UN' 用於更新新值。  
  
-   當您要求旗標時，更新顯示為作業碼後之位元資料行的旗標，並以 *@update_flag_list* 參數中指定的順序顯示。 這些資料行的命名方式是將 '_uflag' 附加到相關聯的資料行名稱。  
  
 如果您的封裝呼叫查詢所有變更的包裝函式，該包裝函式也會傳回 __CDC_STARTLSN 和 \__CDC_SEQVAL 資料行。 這兩個資料行會分別成為結果集的第一和第二個資料行。 此包裝函數也會根據這兩個資料行，排序結果集。  
  
## <a name="writing-your-own-table-value-function"></a>撰寫您自己的資料表值函式  
 您也可以改用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 撰寫呼叫異動資料擷取查詢函數的資料表值包裝函式，並將資料表值包裝函式儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中。 如需如何建立 Transact-SQL 函數的詳細資訊，請參閱 [CREATE FUNCTION &#40;Transact-SQL &#41;](../../t-sql/statements/create-function-transact-sql.md)。  
  
 下列範例定義的資料表值函式可從 Customer 資料表中擷取指定之變更間隔的變更。 此函數會使用異動資料擷取函數，將 **datetime** 值對應到變更資料表在內部使用的二進位記錄序號 (LSN) 值。 此函數也會處理數個特殊狀況：  
  
-   針對開始時間傳遞 null 值時，此函數會使用最早可用的值。  
  
-   針對結束時間傳遞 null 值時，此函數會使用最晚可用的值。  
  
-   當開始 LSN 等於結束 LSN (通常表示沒有所選間隔的記錄) 時，此函數會結束。  
  
### <a name="example-of-a-table-value-function-that-queries-for-change-data"></a>查詢變更資料之資料表值函式的範例  
  
```  
CREATE function CDCSample.uf_Customer (  
     @start_time datetime  
    ,@end_time datetime  
)  
returns @Customer table (  
     CustomerID int  
    ,TerritoryID int  
    ,CustomerType nchar(1)  
    ,rowguid uniqueidentifier  
    ,ModifiedDate datetime  
    ,CDC_OPERATION varchar(1)  
) as  
begin  
    declare @from_lsn binary(10), @to_lsn binary(10)  
  
    if (@start_time is null)  
        select @from_lsn = sys.fn_cdc_get_min_lsn('Customer')  
    else  
        select @from_lsn = sys.fn_cdc_increment_lsn(sys.fn_cdc_map_time_to_lsn('largest less than or equal',@start_time))  
  
    if (@end_time is null)  
        select @to_lsn = sys.fn_cdc_get_max_lsn()  
    else  
        select @to_lsn = sys.fn_cdc_map_time_to_lsn('largest less than or equal',@end_time)  
  
    if (@from_lsn = sys.fn_cdc_increment_lsn(@to_lsn))  
        return  
  
    -- Query for change data  
    insert into @Customer  
    select   
        CustomerID,      
        TerritoryID,   
        CustomerType,   
        rowguid,   
        ModifiedDate,   
        case __$operation  
                when 1 then 'D'  
                when 2 then 'I'  
                when 4 then 'U'  
                else null  
         end as CDC_OPERATION  
    from   
        cdc.fn_cdc_get_net_changes_Customer(@from_lsn, @to_lsn, 'all')  
  
    return  
end   
go  
  
```  
  
### <a name="retrieving-additional-metadata-with-the-change-data"></a>擷取包含異動資料的其他中繼資料  
 雖然之前顯示之使用者建立的資料表值函式僅使用 **__$operation** 資料行，但 **cdc.fn_cdc_get_net_changes_<capture_instance>** 函式會針對每個變更資料列傳回四個中繼資料。 如果您要在資料流程中使用這些值，您可以傳回它們，當做資料表值包裝函數的其他資料行。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**__$start_lsn**|**binary(10)**|與變更之認可交易相關聯的 LSN。<br /><br /> 在相同交易中認可的所有變更都會共用相同的認可 LSN。 例如，如果來源資料表上的更新作業修改了兩個不同的資料列，此變更資料表將會包含四個資料列 (其中兩個是舊值，而另外兩個是新值)，而且每個資料列都包含相同的 **__$start_lsn** 值。|  
|**__$seqval**|**binary(10)**|用來排序交易內資料列變更的序列值。|  
|**__$operation**|**int**|與變更相關聯的資料操作語言 (DML) 作業。 可以是下列其中一項：<br /><br /> 1 = 刪除<br /><br /> 2 = 插入<br /><br /> 3 = 更新 (更新作業之前的值)。<br /><br /> 4 = 更新 (更新作業之後的值)。|  
|**__$update_mask**|**varbinary(128)**|位元遮罩，可根據變更資料表的資料行序數識別這些變更的資料行。 如果您必須判斷已經變更的資料行，可以檢查這個值。|  
|**\<擷取的來源資料表資料行>**|變化|這個函數所傳回的其餘資料行都是建立擷取執行個體時，在來源資料表中識別成擷取資料行的資料行。 如果擷取的資料行清單中沒有以序數指定任何資料行，就會傳回來源資料表中的所有資料行。|  
  
 如需詳細資訊，請參閱 [cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)。  
  
## <a name="next-step"></a>下一個步驟  
 建立查詢變更資料的資料表值函式後，下一個步驟是開始在封裝中設計資料流程。  
  
 **下一個主題：** [擷取與了解變更資料](../../integration-services/change-data-capture/retrieve-and-understand-the-change-data.md)  
  
  
