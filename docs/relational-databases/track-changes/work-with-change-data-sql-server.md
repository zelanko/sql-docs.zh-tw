---
title: 使用變更資料
ms.custom: seo-dt-2019
ms.date: 01/02/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- change data [SQL Server]
- change data capture [SQL Server], query function scenarios
- change data capture [SQL Server], LSN boundaries
- change data capture [SQL Server], query functions
ms.assetid: 5346b852-1af8-4080-b278-12efb9b735eb
author: rothja
ms.author: jroth
ms.openlocfilehash: 18002782d7d34b88706b227cf8ac828f9da4976a
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85889088"
---
# <a name="work-with-change-data-sql-server"></a>使用變更資料 (SQL Server)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]
  異動資料擷取取用者會透過資料表值函式 (TVF) 取得變更資料。 這些函數的所有查詢都需要使用兩個參數來定義開發傳回的結果集時適合用於考量的記錄序號 (LSN) 範圍。 限制間隔的上下 LSN 值會被視為包含在間隔內部。  
  
 我們提供了許多函數，可協助您判斷查詢 TVF 時所使用的適當 LSN 值。 [sys.fn_cdc_get_min_lsn](../../relational-databases/system-functions/sys-fn-cdc-get-min-lsn-transact-sql.md) 函數會傳回與擷取執行個體有效性間隔相關聯的最小 LSN。 有效性間隔就是擷取執行個體目前可以使用變更資料的時間間隔。 [sys.fn_cdc_get_max_lsn](../../relational-databases/system-functions/sys-fn-cdc-get-max-lsn-transact-sql.md) 函數會傳回有效性間隔中的最大 LSN。 [sys.fn_cdc_map_time_to_lsn](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md) 和 [sys.fn_cdc_map_lsn_to_time](../../relational-databases/system-functions/sys-fn-cdc-map-lsn-to-time-transact-sql.md) 函數可用來協助您將 LSN 值放置在傳統時間表上。 由於異動資料擷取會使用封閉的查詢間隔，因此有時候必須在序列中產生下一個 LSN 值，以便確保連續的查詢視窗中不會有重複的變更。 當您需要針對 LSN 值進行累加式調整時， [sys.fn_cdc_increment_lsn](../../relational-databases/system-functions/sys-fn-cdc-increment-lsn-transact-sql.md) 和 [sys.fn_cdc_decrement_lsn](../../relational-databases/system-functions/sys-fn-cdc-decrement-lsn-transact-sql.md) 函數就很有用。  
  
##  <a name="validating-lsn-boundaries"></a><a name="LSN"></a> 驗證 LSN 界限  
 我們建議您先驗證即將用於 TVF 查詢中的 LSN 界限，然後再加以使用。 Null 端點或位於擷取執行個體有效性間隔外部的端點將會強制異動資料擷取 TVF 傳回錯誤。  
  
 例如，當用來定義查詢間隔的參數無效或超出範圍，或者資料列篩選選項無效時，系統就會針對所有變更的查詢傳回下列錯誤。  
  
 `Msg 313, Level 16, State 3, Line 1`  
  
 `An insufficient number of arguments were supplied for the procedure or function cdc.fn_cdc_get_all_changes_ ...`  
  
 針對 **net changes** 查詢傳回的對應錯誤如下所示：  
  
 `Msg 313, Level 16, State 3, Line 1`  
  
 `An insufficient number of arguments were supplied for the procedure or function cdc.fn_cdc_get_net_changes_ ...`  
  
> [!NOTE]  
>  「訊息 313」的訊息確實產生誤導而且並未傳達失敗的實際原因。 這種不當的使用方式起因為無法從 TVF 內部引發明確的錯誤。 不過，我們認為傳回可辨識 (但不正確) 錯誤的價值會比單獨傳回空白結果的價值更高。 空白的結果集與沒有傳回任何變更的有效查詢並無差別。  
  
 查詢所有變更時，授權失敗會傳回失敗，如下所示：  
  
 `Msg 229, Level 14, State 5, Line 1`  
  
 `The SELECT permission was denied on the object 'fn_cdc_get_all_changes_...', database 'MyDB', schema 'cdc'.`  
  
 查詢淨變更的情況也是如此：  
  
 `Msg 229, Level 14, State 5, Line 1`  
  
 `The SELECT permission was denied on the object fn_cdc_get_net_changes_...', database 'MyDB', schema 'cdc'.`  
  
 如需如何攔截這些已知 TVF 錯誤的示範，並且傳回有關失敗的更有意義資訊，請參閱「使用 TRY CATCH 來列舉淨變更」範本。  
  
> [!NOTE]  
>  若要在 SQL Server Management Studio 中找出異動資料擷取範本，請在 [檢視]  功能表上，按一下 [範本總管]  、展開 [SQL Server 範本]  ，然後展開 [異動資料擷取]  資料夾。  
  
##  <a name="query-functions"></a><a name="Functions"></a> 查詢函數  
 系統會根據所追蹤之來源資料表的特性以及其擷取執行個體的設定方式，產生一個或兩個 TVF 以便查詢變更資料。  
  
-   [cdc.fn_cdc_get_all_changes_<capture_instance>](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md) 函數會傳回在指定的間隔中發生的所有變更。 系統一定會產生這個函數。 傳回的項目一律會經過排序 (先依據變更的交易認可 LSN，然後再依據變更在交易內部排列順序的值)。 根據選擇的資料列篩選選項，系統會在更新時傳回最後一個資料列 (資料列篩選選項 "all") 或在更新時傳回全新和舊的值 (資料列篩選選項 "all update old")。  
  
-   啟用來源資料表時，如果將參數 @supports_net_changes 設定為 1，則會產生函式 [cdc.fn_cdc_get_net_changes_<擷取執行個體>](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)。  
  
    > [!NOTE]  
    >  只有當來源資料表具有已定義的主索引鍵，或者 @index_name 參數已經用來識別唯一的索引時，才支援這個選項。  
  
     **netchanges** 函數會針對每個已修改的來源資料表資料列傳回一項變更。 如果在指定的間隔期間記錄了資料列的多個變更，資料行值將會反映資料列的最終內容。 為了正確識別更新目標環境所需的作業，TVF 必須同時考慮資料列在間隔期間的初始作業，以及資料列的最終作業。 指定資料列篩選選項 'all' 時， **淨變更** 查詢所傳回的作業就是插入、刪除或更新 (新值)。 此選項永遠會將更新遮罩傳回為 Null，因為存在與計算彙總遮罩相關聯的成本。 如果您需要反映資料列之所有變更的彙總遮罩，請使用 'all with mask' 選項。 如果下游處理不需要區分插入和更新，請使用 'all with merge' 選項。 在此情況下，作業值只會使用兩個值：1 用於刪除，而 5 用於可以是插入或更新的作業。 這個選項可以排除判斷衍生之作業是插入還是更新的額外處理需求，因此可以在不需要加以區分時，增進查詢的效能。  
  
 從查詢函數傳回的更新遮罩是一種精簡型的表示法，它會識別在變更資料之資料列中變更的所有資料行。 一般而言，只有擷取資料行的小型子集需要這個資訊。 但是，如果使用這些函數，將有助於以應用程式更可直接應用的形式，從遮罩擷取資訊。 [sys.fn_cdc_get_column_ordinal](../../relational-databases/system-functions/sys-fn-cdc-get-column-ordinal-transact-sql.md) 函數會針對給定的擷取執行個體，傳回具名資料行的序數位置，而 [sys.fn_cdc_is_bit_set](../../relational-databases/system-functions/sys-fn-cdc-is-bit-set-transact-sql.md) 函數則會根據傳入函數呼叫中的序數，傳回提供之遮罩中的同位位元。 同時，這兩個函數可以針對變更資料的要求，有效率地擷取並傳回更新遮罩的資訊。 如需如何使用這些函數的示範，請參閱「使用 All With Mask 來列舉淨變更」範本。  
  
##  <a name="query-function-scenarios"></a><a name="Scenarios"></a> 查詢函數狀況  
 下列各節將描述使用 cdc.fn_cdc_get_all_changes_<capture_instance> 和 cdc.fn_cdc_get_net_changes_<capture_instance> 查詢函數來查詢異動資料擷取資料的一般狀況。  
  
### <a name="querying-for-all-changes-within-the-capture-instance-validity-interval"></a>在擷取執行個體有效性間隔內查詢所有變更  
 變更資料最直接的要求就是在擷取執行個體有效性間隔中傳回所有目前變更資料。 若要提出這項要求，請先判斷有效性間隔的 LSN 下限與上限。 然後，請使用這些值來識別傳遞給 cdc.fn_cdc_get_all_changes_<擷取執行個體> 或 cdc.fn_cdc_get_net_changes_<擷取執行個體> 查詢函式的 @from_lsn 和 @to_lsn 參數。 您可以使用 [sys.fn_cdc_get_min_lsn](../../relational-databases/system-functions/sys-fn-cdc-get-min-lsn-transact-sql.md) 函數來取得下限，而使用 [sys.fn_cdc_get_max_lsn](../../relational-databases/system-functions/sys-fn-cdc-get-max-lsn-transact-sql.md) 函數來取得上限。 如需使用 cdc.fn_cdc_get_all_changes_<capture_instance> 查詢函數來查詢所有目前有效變更的範例程式碼，請參閱「列舉有效範圍的所有變更」範本。 如需使用 cdc.fn_cdc_get_net_changes_<capture_instance> 函數的類似範例，請參閱「列舉有效範圍的淨變更」範本。  
  
### <a name="querying-for-all-new-changes-since-the-last-set-of-changes"></a>查詢自從上一組變更以來的所有新變更  
 對於一般應用程式而言，查詢變更資料是持續進行的程序，並且針對自從上一個要求以來發生的所有變更提出定期要求。 您可以針對這類查詢使用 [sys.fn_cdc_increment_lsn](../../relational-databases/system-functions/sys-fn-cdc-increment-lsn-transact-sql.md) 函數，以便從上一個查詢的上限衍生出目前查詢的下限。 這個方法可確保不會重複任何資料列，因為查詢間隔永遠會被視為封閉的間隔，其中兩個端點都包含在間隔中。 然後，您可以使用 [sys.fn_cdc_get_max_lsn](../../relational-databases/system-functions/sys-fn-cdc-get-max-lsn-transact-sql.md) 函數來取得新要求間隔的高端點。 如需有系統地移動查詢視窗來取得自從上一個要求以來之所有變更的範例程式碼，請參閱「列舉自從上一個要求以來的所有變更」範本。  
  
### <a name="querying-for-all-new-changes-up-until-now"></a>查詢至今為止的所有新變更  
 針對查詢函數所傳回之變更放置的一般條件約束是僅包含上一個要求到目前日期和時間之間發生的變更。 若為這種查詢，您可以將 sys.fn_cdc_increment_lsn 函式套用至上一個要求所使用的 @from_lsn 值，以便判斷下限。 由於時間間隔的上限會表示成特定時間點，所以它必須轉換成 LSN 值，然後才能讓查詢函數使用。 您必須確定擷取處理序已經處理透過指定之上限所認可的所有變更，然後此日期時間值才能轉換成對應的 LSN 值。 這是確保所有合格變更都已經傳播至變更資料表的必要作業。 進行此作業的其中一種方式為建構定期檢查的等候迴圈，以便查看針對任何資料庫變更資料表所記錄的目前最大認可 LSN 是否超過要求間隔的所需結束時間。  
  
 在延遲迴圈確認擷取處理序已經處理所有相關的記錄項目之後，請使用 [sys.fn_cdc_map_time_to_lsn](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md) 函數來判斷表示成 LSN 值的新高端點。 若要確定已擷取透過指定之時間認可的所有項目，請呼叫 sys.fn_cdc_map_time_to_lsn 函數並使用 'largest less than or equal' 選項。  
  
> [!NOTE]  
>  在沒有活動的期間，空的項目會加入至 cdc.lsn_time_mapping 資料表，以便表示擷取處理序已經處理這些變更 (直到給定的認可時間)。 這樣會避免在完全沒有任何最近的變更要處理時，顯示擷取處理序已經落後。  
  
 「列舉至今為止的所有變更」範本將示範如何使用先前的策略來查詢變更資料。  
  
### <a name="adding-a-commit-time-to-an-all-changes-result-set"></a>將認可時間加入至所有變更結果集  
 [cdc.lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md)資料表提供在資料庫變更資料表中具有相關聯項目之每筆交易的認可時間。 您可以透過聯結傳入所有變更之要求中的 __$start_lsn 值與 cdc.lsn_time_mapping 資料表項目的 start_lsn 值，傳回 tran_end_time 以及變更資料，以便使用位於來源之交易的認可時間為變更加上戳記。 「將認可時間附加至所有變更結果集」範本將示範如何執行這項聯結。  
  
### <a name="joining-change-data-with-other-data-from-the-same-transaction"></a>聯結變更資料與來自相同交易的其他資料  
 有時候，在來源認可交易時，聯結變更資料與其他所蒐集的交易相關資訊會很有用。 cdc.lsn_time_mapping 資料表中的 tran_begin_lsn 資料行會提供執行這類聯結所需的資訊。 更新來源時，來自 [sys.dm_tran_database_transactions](../../relational-databases/system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md) 系統動態檢視的 database_transaction_begin_lsn 值必須與要和變更資料聯結的任何其他資訊一起儲存。 您可以使用 fn_convertnumericlsntobinary 函數來比較 database_transaction_begin_lsn 與 tran_begin_lsn 值。 「建立函數 fn_convertnumericlsntobinary」範本會提供要建立此函數的程式碼。 「使用給定的 tran_begin_lsn 來傳回所有變更」範本將示範如何完成此聯結。  
  
### <a name="querying-using-datetime-wrapper-functions"></a>使用日期時間包裝函數來查詢  
 查詢變更資料的一般應用程式狀況是使用以日期時間值所限定的滑動視窗來定期要求變更資料。 若為這種取用者類別，異動資料擷取會提供 [sys.sp_cdc_generate_wrapper_function](../../relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql.md) 預存程序，以便產生指令碼來建立異動資料擷取查詢函數的自訂包裝函數。 這些自訂包裝函數可讓查詢間隔表示成日期時間組。  
  
 此預存程序的呼叫選項可讓您針對呼叫者可存取的所有擷取執行個體或只針對指定的擷取執行個體產生包裝函數。 支援的選項還包括能夠指定擷取間隔的高端點應該開啟或關閉、哪些可用的擷取資料行應該包含在結果集中，以及哪些包含資料行應該具有相關聯的更新旗標。 此程序會傳回含有兩個資料行的結果集：產生的函數名稱 (可從擷取執行個體名稱衍生出) 和包裝函數預存程序的建立陳述式。 系統一定會產生可包裝所有變更查詢的函數。 如果建立擷取執行個體時設定 @supports_net_changes 參數，也會產生可包裝淨變更函式的函式。  
  
 應用程式設計工具必須負責呼叫指令碼產生預存程序來產生包裝函數預存程序的建立陳述式，以及執行產生的建立指令碼來建立這些函數。 這項作業不會在建立擷取執行個體時自動進行。  
  
 日期時間包裝函數是由使用者所擁有，並非建立在呼叫者的預設結構描述中。 產生的函數不需要修改就可適用於大部分使用者。 不過，建立此函數之前，您隨時都可以將進一步的自訂套用至產生的指令碼。  
  
 包裝所有變更查詢之函數的名稱是 fn_all_changes_ 後面接著擷取執行個體名稱。 用於淨變更包裝函數的前置詞為 fn_net_changes_。 這兩個函數都會接受三個引數，就如同其相關聯的異動資料擷取 TVF 一樣。 不過，這些包裝函數的查詢間隔是以兩個日期時間值 (而非兩個 LSN 值) 所限定。 這兩組函式的 @row_filter_option 參數都相同。  
  
 產生的包裝函式支援下列有系統地查核異動資料擷取時間表的慣例：先前間隔的 @end_time 參數應該要當作後續間隔的 @start_time 參數使用。 此包裝函數會負責將日期時間值對應至 LSN 值，並且確保遵循此慣例時，不會遺漏或重複任何資料。  
  
 您可以產生包裝函數來支援指定之查詢視窗上的封閉上限或開放上限。 也就是說，呼叫者可以指定具有認可時間的項目是否等於要包含在間隔內之擷取間隔的上限。 預設會包含上限。  
  
 當產生的查詢 TVF 失敗時，如果針對 @from_lsn 值或 @to_lsn 值提供 Null 值，日期時間包裝函式就會使用 Null 來允許日期時間包裝函式傳回所有目前的變更。 也就是說，如果 Null 當做查詢視窗的低端點傳遞至日期時間包裝函數，擷取執行個體有效性間隔的低端點就會用於套用至查詢 TVF 的基礎 SELECT 陳述式中。 同樣地，如果 Null 當做查詢視窗的高端點傳遞，擷取執行個體有效性間隔的高端點就會在從查詢 TVF 中選取時使用。  
  
 包裝函數所傳回的結果集包括所有要求的資料行，後面接著作業資料行，而此資料行會記錄成一或兩個字元，以便識別與資料列相關聯的作業。 如果已經要求更新旗標，它們就會按照 @update_flag_list 參數中指定的順序，在作業碼之後顯示成位元資料行。 如需自訂產生之日期時間包裝函式的呼叫選項資訊，請參閱 [sys.sp_cdc_generate_wrapper_function &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql.md)。  
  
 「使用更新旗標來具現化包裝函數 TVF」範本會示範如何自訂產生的包裝函數，以便將指定之資料行的更新旗標附加至淨變更查詢所傳回的結果集。 「具現化結構描述的 CDC 包裝函數 TVF」範本會示範如何針對所有擷取執行個體 (為給定之資料庫結構描述中的來源資料表所建立)，具現化查詢 TVF 的日期時間包裝函數。  
  
 如需使用日期時間包裝函數來查詢變更資料的範例，請參閱「使用包裝函數搭配更新旗標來取得淨變更」範本。 這個範本會示範如何在包裝函數設定成傳回更新旗標時，使用包裝函數來查詢淨變更。 請注意，若要讓基礎查詢函數在更新時傳回非 Null 更新遮罩，就必須使用資料列篩選選項 'all with mask'。 Null 值會傳遞成日期時間間隔的下限和上限，以便通知函數在執行基礎 LSN 架構查詢時，使用擷取執行個體之有效性間隔的低端點和高端點。 此查詢會針對在擷取執行個體之有效範圍內發生的每個來源資料列修改，傳回一個資料列。  
  
### <a name="using-the-datetime-wrapper-functions-to-transition-between-capture-instances"></a>使用日期時間包裝函數在擷取執行體之間轉換  
 對於單一追蹤來源資料表而言，異動資料擷取最多支援兩個擷取執行個體。 這項功能的主要用途是在來源資料表的資料定義語言 (DDL) 變更擴充可用於追蹤的資料行集合時，容納多個擷取執行個體之間的轉換。 轉換成新的擷取執行個體時，其中一種避免較高應用程式層級變更基礎查詢函數名稱的方式是使用包裝函數來包裝基礎呼叫。 然後，請確定包裝函數的名稱維持不變。 進行切換時，可能會卸除舊的包裝函數，而且建立具有相同名稱的新包裝函數，並且參考新的查詢函數。 您可以透過先將產生的指令碼修改成建立相同名稱的包裝函數，切換至新的擷取執行個體，而不影響較高的應用程式層。  
  
## <a name="see-also"></a>另請參閱  
 [追蹤資料變更 &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)   
 [關於異動資料擷取 &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)   
 [啟用和停用異動資料擷取 &#40;SQL Server&#41;](../../relational-databases/track-changes/enable-and-disable-change-data-capture-sql-server.md)   
 [管理和監視異動資料擷取 &#40;SQL Server&#41;](../../relational-databases/track-changes/administer-and-monitor-change-data-capture-sql-server.md)  
  
  
