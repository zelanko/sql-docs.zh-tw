---
title: "資料庫一致性檢查 (DBCC) for Analysis Services |Microsoft 文件"
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 28714c32-718f-4f31-a597-b3289b04b864
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8348c7c3ee60d7032f9c8af373ce5b9e1a026f8f
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2018
---
# <a name="database-consistency-checker-dbcc-for-analysis-services"></a>Analysis Services 的 database Consistency Checker (DBCC)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
DBCC 提供適用於 Analysis Services 執行個體上之多維度和表格式資料庫的隨選驗證。 您可以在 SQL Server Management Studio (SSMS) 的 MDX 或 XMLA 查詢視窗中執行 DBCC，並在 SSMS 的 SQL Server Profiler 或 xEvent 工作階段中追蹤 DBCC 輸出。  
此命令會接受物件定義，並傳回空的結果集或詳細錯誤資訊 (如果物件已損毀)。   在本文中，您將了解如何執行命令、解譯結果，以及解決任何發生的問題。  
  
 對於表格式資料庫，DBCC 所執行的一致性檢查相當於每次重新載入、同步處理或還原資料庫時自動發生的內建驗證。  相反地，多維度資料庫的一致性檢查只會在您依照需求執行 DBCC 時發生。  
  
 驗證檢查的範圍會隨著模式而改變；表格式資料庫需接受範圍較為廣泛的檢查。  
 DBCC 工作負載的特性也會因伺服器模式不同而有所差異。 多維度資料庫上的檢查作業牽涉到從磁碟讀取資料、建構暫存索引以供比對實際索引之用；這些作業都需要花費相當長的時間才能完成。  
  
 DBCC 的命令語法需使用物件中繼資料，這些資料會隨著要檢查的資料庫類型不同而改變︰  
  
-   諸如 **cubeID**、 **measuregroupID**和 **partitionID**等多維度模型建構描述多維度 + SQL Server 2016 之前的表格式 1100 或 1103 相容性層級資料庫。  
  
-   中繼資料的描述元包含新的表格式模型資料庫，相容性層級 1200年 （含） 以上喜歡**TableName**和**PartitionName**。  
  
 只要資料庫是在 SQL Server 2016 執行個體上執行，DBCC for Analysis Services 便能在任何相容性層級的任何 Analysis Services 資料庫上執行。 只要確認您針對每個資料庫類型使用正確的命令語法即可。  
  
> [!NOTE]  
>  如果您熟悉 [DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)，很快地您會發現 Analysis Services 中的 DBCC 範圍較狹隘。 Analysis Services 中的 DBCC 是專門針對整個資料庫或個別物件回報資料損毀的單一命令。 如果您需要將其他工作 (如收集資訊) 納入考量，請嘗試改用 AMO PowerShell 或 XMLA 指令碼。 如需詳細資訊連結，請參閱 [Monitor an Analysis Services Instance](../../analysis-services/instances/monitor-an-analysis-services-instance.md) 。  
  
## <a name="permission-requirements"></a>權限需求  
 您必須是 Analysis Services 資料庫或伺服器管理員 (伺服器角色的成員) 才能執行命令。 如需相關指示，請參閱[授與資料庫權限 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md) 或[將伺服器系統管理員權限授與 Analysis Services 執行個體](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md)。  
  
## <a name="command-syntax"></a>命令語法 
 位於 1200年的表格式資料庫及更高的相容性層級使用表格式中繼資料的物件定義。 下列範例說明在 SQL Server 2016 功能層級建立之表格式資料庫的完整 DBCC 語法。  
  
 兩種語法之間的主要差異包括較新的 XMLA 命名空間，不\<物件 > 項目，且沒有\<模型 > （沒有每個資料庫仍然只有一個模型） 的項目。  
  
```  
<DBCC xmlns="http://schemas.microsoft.com/analysisservices/2014/engine">  
     <DatabaseID>MyTabular1200DB_7811b5d8-c407-4203-8793-12e16c3d1b9b</DatabaseID>  
     <TableName>FactSales</TableName>  
     <PartitionName>FactSales 4</PartitionName>  
</DBCC>  
```  
  
 您可以略過較低層級的物件 (如資料表或分割區的名稱)，以便檢查整個結構描述。  
  
 在 Management Studio 中，您可以透過每個物件的屬性頁取得物件名稱和 DatabaseID。  
  
## <a name="command-syntax-for-multidimensional-and-tabular-110x-databases"></a>多維度和表格式 110x 資料庫的命令語法  
 DBCC 在多維度及表格式 1100 和 1103 資料庫中使用相同的語法。 您可以針對特定資料庫物件 (包括整個資料庫) 執行 DBCC。 如需物件定義的詳細資訊，請參閱 [Object 元素 &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)。  
  
```  
<DBCC xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
     <Object>  
          <DatabaseID>AdventureWorksDW2014Multidimensional-EE</DatabaseID>  
          <CubeID>Adventure Works</CubeID>  
          <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
          <PartitionID>Internet_Sales_2006</PartitionID>  
     </Object>  
</DBCC>  
  
```  
  
 若要針對上至物件鏈結的物件執行 DBCC，請刪除任何不需要的低層級物件識別碼項目︰  
  
```  
<DBCC xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
     <Object>  
          <DatabaseID>AdventureWorksDW2014Multidimensional-EE</DatabaseID>  
          <CubeID>Adventure Works</CubeID>  
     </Object>  
</DBCC>  
  
```  
  
 對於表格式 110x 資料庫，物件定義語法會在 Process 命令的語法 (具體來說，關於資料表與維度和量值群組的對應方式) 之後模型化。  
  
-   **CubeID** 對應至模型識別碼，其為 **Model**。  
  
-   **MeasureGroupID** 對應至資料表識別碼。  
  
-   **PartitionID** 對應至分割區識別碼。  
  
## <a name="usage"></a>使用方式  
 在 SQL Server Management Studio 中，您可以使用 MDX 或 XMLA 查詢視窗來叫用 DBCC。 此外，您還可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Profiler 或 Analysis Services Xevent 來檢視 DBCC 輸出。 請注意，系統不會向 Windows 應用程式事件記錄檔或 msmdsrv.log 檔案報告 SSAS DBCC 訊息。  
  
 DBCC 會檢查實體資料損毀，以及區段出現被遺棄成員時發生的邏輯資料損毀。 資料庫必須經過處理，您才能執行 DBCC。 它會略過遠端、空白或未處理的分割區。  
  
 命令會在讀取交易中執行，因此可以透過強制認可逾時排除。 分割區檢查會以平行方式執行。  
  
 您可能需要重新啟動服務，才能收取上次服務重新啟動之後所發生的任何損毀錯誤。 重新連接伺服器不足以收取這些變更。  
  
### <a name="run-dbcc-commands-in-management-studio"></a>在 Management Studio 中執行 DBCC 命令  
 針對臨機操作查詢，請在 SQL Server Management Studio 中開啟 MDX 或 XMLA 查詢視窗。 若要這樣做，請以滑鼠右鍵按一下資料庫 | [新增查詢] | [XMLA] 以執行命令及讀取輸出。  
  
 ![在 Management Studio 中的 DBCC XML 命令](../../analysis-services/instances/media/ssas-dbcc-ssms.gif "在 Management Studio 中的 DBCC XML 命令")  
  
 如果沒有偵測到任何問題，[結果] 索引標籤會指出空白的結果集 (如螢幕擷取畫面所示)。  
  
 [訊息] 索引標籤能提供詳細資訊，但對於較小型的資料庫來說，不見得每次都可靠。 狀態訊息有時候會遭到修剪，雖然它們指出命令已完成，但卻沒有每個物件的狀態檢查訊息。 一般訊息報表的外觀與以下範例相似。  
  
 **從 DBCC 回報的 Cube 驗證檢查訊息**  
  
```  
Executing the query ...  
READS, 0  
READ_KB, 0  
WRITES, 0  
WRITE_KB, 0  
CPU_TIME_MS, 0  
ROWS_SCANNED, 0  
ROWS_RETURNED, 0  
  
<DBCC xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
<Object>  
<DatabaseID>AdventureWorksDW2014Multidimensional-EE</DatabaseID>  
<CubeID>Adventure Works</CubeID>  
</Object>  
</DBCC>  
Started checking segment indexes for the 'Internet_Sales_2011' partition.  
Started checking segment indexes for the 'Internet_Sales_2012' partition.  
Finished checking segment indexes for the 'Internet_Sales_2011' partition.  
Started checking segment indexes for the 'Internet_Sales_2013' partition.  
Finished checking segment indexes for the 'Internet_Sales_2012' partition.  
Started checking segment indexes for the 'Internet_Sales_2014' partition.  
Started checking segment indexes for the 'Internet_Orders_2011' partition.  
Finished checking segment indexes for the 'Internet_Sales_2014' partition.  
Started checking segment indexes for the 'Internet_Orders_2012' partition.  
Started checking segment indexes for the 'Internet_Orders_2013' partition.  
Finished checking segment indexes for the 'Internet_Orders_2012' partition.  
...   
Run complete  
  
```  
  
 **針對舊版 Analysis Services 執行 DBCC 時的輸出**  
  
 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 執行個體上執行的資料庫僅支援 DBCC。 在較舊的系統上執行命令會傳回此錯誤。  
  
```  
Executing the query ...  
The DBCC element at line 7, column 87 (namespace http://schemas.microsoft.com/analysisservices/2003/engine) cannot appear under Envelope/Body/Execute/Command.  
Execution complete  
  
```  
  
### <a name="trace-dbcc-output-in-sql-server-profiler-2016"></a>在 SQL Server Profiler 2016 中追蹤 DBCC 輸出  
 您可以在包含進度報表事件 (進度報表開始、進度報表目前事件、進度報表結束和進度報表錯誤) 的 Profiler 追蹤內檢視 DBCC 輸出。  
  
1.  啟動追蹤。 如需搭配使用 SQL Server Profiler 和 Analysis Services 的協助，請參閱 [Use SQL Server Profiler to Monitor Analysis Services](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md) 。  
  
2.  選擇 **Command Begin** 和 [命令結束]  ，再加上任一或所有 [進度報表]  事件。  
  
3.  使用上一節所提供的語法，在 Management Studio 的 XMLA 或 MDX 查詢視窗中執行 DBCC 命令。  
  
4.  在 SQL Server Profiler 中，DBCC 活動係透過擁有 DBCC 事件子類別的 **Command** 事件來表示︰  
  
     ![ssas-dbcc-profiler-eventsubclass](../../analysis-services/instances/media/ssas-dbcc-profiler-eventsubclass.PNG "ssas-dbcc-profiler-eventsubclass")  
  
     事件代碼 32 代表 DBCC 執行。  
  
     事件代碼 64 代表針對個別物件的 DBCC 進度報表。  
  
     事件代碼 63 代表多維度物件的區段檢查。  
  
     對於這兩個事件子類別，請檢閱 **TextData** 值以取得 DBCC 傳回的訊息。  
  
     狀態訊息的開頭 」 的一致性檢查\<物件 >"，"已開始檢查\<物件 >"，或 「 已完成檢查\<物件 > 」。  
  
    > [!NOTE]  
    >  在 CTP 3.0 中，物件是由內部名稱來加以識別。 類別階層架構，例如字集 H$ 分類-\<objectID >。 在後續的 CTP 中，內部名稱應取代為使用者易記名稱。  
  
     錯誤訊息如下所示。  
  
### <a name="trace-dbcc-output-in-an-xevent-session-in-ssms"></a>SSMS 中 xEvent 工作階段的追蹤 DBCC 輸出  
 擴充事件工作階段可以使用 Profiler 事件或 xEvent。 如需加入 **Command** 和 **Progress Report** 事件的指引，請參閱上一節。  
  
1.  以滑鼠右鍵按一下資料庫以啟動工作階段 > [管理] > [擴充事件] >  [工作階段] > [新增工作階段]。 如需詳細資訊，請參閱  [Monitor Analysis Services with SQL Server Extended Events](../../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md) 。  
  
2.  選擇 Profiler 事件類別目錄的任一或所有 **進度報表** 事件，或 PureXevent 類別目錄的 **RequestProgress** 事件。  
  
3.  使用上一節所提供的語法，在 Management Studio 的 XMLA 或 MDX 查詢視窗中執行 DBCC 命令。  
  
4.  在 SSMS 中，重新整理 Sessions 資料夾。 以用滑鼠右鍵按一下工作階段名稱 > [觀看即時資料]。  
  
5.  檢閱 DBCC 傳回之訊息的 TextData 值。  TextData 是事件欄位的屬性，它能顯示事件傳回的狀態和錯誤訊息。  
  
     狀態訊息的開頭 」 的一致性檢查\<物件 >"，"已開始檢查\<物件 >"，或 「 已完成檢查\<物件 > 」。  
  
     錯誤訊息如下所示。  
  
## <a name="reference-consistency-checks-and-errors-for-multidimensional-databases"></a>參考資料︰多維度資料庫的一致性檢查和錯誤  
 多維度資料庫的分割區索引是唯一需要驗證的部分。  在執行期間，DBCC 會建立每個分割區的暫存索引，再與磁碟上的保存索引比較。  建立暫存索引需要讀取磁碟上的所有分割區資料，然後將暫存索引保存在記憶體中，以供比較之用。 如果遭遇到額外的工作負載，伺服器可能會在 DBCC 執行期間發生大量的磁碟 IO 和記憶體耗用量。  
  
 多維度索引損毀偵測包含下列檢查。 下表中的錯誤會在發生物件層級失敗時出現在 xEvent 或 Profiler 追蹤內。  
  
||||  
|-|-|-|  
|**物件**|**DBCC 檢查描述**|**失敗錯誤**|  
|分割區索引|檢查區段統計資料和索引。<br /><br /> 比較暫存分割區索引中每個成員的識別碼，以及儲存在磁碟上的分割區統計資料。  如果成員位於暫存索引中，且其資料識別碼值超出儲存在磁碟上之分割區索引統計資料的範圍，檢查會將索引的統計資料視為損毀。|分割區區段統計資料已損毀。|  
|分割區索引|驗證中繼資料。<br /><br /> 確認暫存索引中的每個成員是否都可以在磁碟的區段索引標頭檔中找到。|分割區區段已損毀。|  
|分割區索引|掃描區段來尋找實體損毀。<br /><br /> 讀取磁碟上的索引檔案以尋找暫存索引中每個成員，並確認索引的大小記錄符合，且相同的資料頁面已標示為具有目前成員的記錄。|分割區區段已損毀。|  
  
## <a name="reference-consistency-checks-and-errors-for-tabular-databases"></a>參考資料︰表格式資料庫的一致性檢查和錯誤  
 下表是針對表格式物件執行之所有一致性檢查的清單，以及當檢查指出毀損時引發的錯誤。 下表中的錯誤會在發生物件層級失敗時出現在 xEvent 或 Profiler 追蹤內。  
  
||||  
|-|-|-|  
|**物件**|**DBCC 檢查描述**|**失敗錯誤**|  
|資料庫|檢查資料庫中的資料表數目。  小於零的值表示損毀。|儲存層發生損毀。 '%{parent/}' 資料庫中的資料表集合已損毀。|  
|資料庫|檢查用來追蹤參考完整性的內部結構，並在大小不正確時擲回錯誤。|資料庫檔案無法通過一致性檢查。|  
|Table|檢查用來判斷資料表是維度資料表或事實資料表的內部值。  超出已知範圍的值表示損毀。|檢查資料表統計資料時資料庫一致性檢查 (DBCC) 失敗。|  
|Table|檢查資料表之區段對應中的分割區數目是否與資料表的已定義分割區數目相符。|儲存層發生損毀。 '%{parent/}' 資料表中的分割區集合已損毀。|  
|Table|如果表格式資料庫是從 PowerPivot for Excel 2010 建立或匯入，且其分割區計數大於一，該狀況將引發錯誤，因為分割區支援是在更新版本中加入，而這就表示損毀。|檢查區段對應時資料庫一致性檢查 (DBCC) 失敗。|  
|資料分割|檢查每個分割區，確認資料區段的數目和區段中每個資料區段的記錄計數，是否與儲存在區段索引中的值相符。|檢查區段對應時資料庫一致性檢查 (DBCC) 失敗。|  
|資料分割|如果記錄、區段或每個區段的記錄總數不正確 (小於零)，或區段數目不符合根據記錄總數計算出來的必要區段數目，便引發錯誤。|檢查區段對應時資料庫一致性檢查 (DBCC) 失敗。|  
|關聯性|如果用來儲存關聯性相關資料的結構不含任何記錄，抑或是如果用於關聯性的資料表名稱為空白，便引發錯誤。|檢查關聯性時資料庫一致性檢查 (DBCC) 失敗。|  
|關聯性|確認主要資料表、主要資料行、外部資料表及外部資料行的名稱是否已設定，且涉及關聯性的資料行和資料表是否可存取。<br /><br /> 確認相關的資料行類型是否有效，且主索引鍵-外部索引鍵值的索引是否能產生有效的查詢結構。|檢查關聯性時資料庫一致性檢查 (DBCC) 失敗。|  
|階層|如果階層的排序次序是不可辨識的值，便引發錯誤。|檢查 '%{hier/}' 階層時資料庫一致性檢查 (DBCC) 失敗。|  
|階層|針對階層執行的檢查取決於使用的階層對應配置內部類型。<br /><br /> 檢查所有階層的已處理狀態是否正確，即階層存放區存在，且適用於資料識別碼至階層位置轉換的資料結構存在。<br /><br /> 假設以上所有檢查均通過，便移動階層結構來確認階層中的每個位置都指向正確的成員。<br />如果有任何未通過的測試，便引發錯誤。|檢查 '%{hier/}' 階層時資料庫一致性檢查 (DBCC) 失敗。|  
|使用者定義階層|檢查階層層級名稱是否已設定。<br /><br /> 如果階層已處理，便檢查內部階層資料存放區內是否有正確的格式。  確認內部階層存放區是否不含任何無效的資料值。<br /><br /> 如果階層標示為未處理，確認此狀態適用於舊資料結構且階層的所有層級均標示為空白。|檢查 '%{hier/}' 階層時資料庫一致性檢查 (DBCC) 失敗。|  
|資料行|如果未將資料行使用的編碼設定成已知的值，便引發錯誤。|檢查資料行統計資料時資料庫一致性檢查 (DBCC) 失敗。|  
|資料行|檢查記憶體中引擎是否已壓縮資料行。|檢查資料行統計資料時資料庫一致性檢查 (DBCC) 失敗。|  
|資料行|檢查資料行的壓縮類型是否為已知的值。|檢查資料行統計資料時資料庫一致性檢查 (DBCC) 失敗。|  
|資料行|當「Token 化」資料行未設定成已知的值時，便引發錯誤。|檢查資料行統計資料時資料庫一致性檢查 (DBCC) 失敗。|  
|資料行|如果儲存的資料行資料字典識別碼範圍與資料字典中的值數目不符或超出允許的範圍，便引發錯誤。|檢查資料字典時資料庫一致性檢查 (DBCC) 失敗。|  
|資料行|檢查資料行的資料區段數目是否與所屬之資料表的資料區段數目相符。|儲存層發生損毀。 '%{parent/}' 資料行中的區段集合已損毀。|  
|資料行|檢查資料行的分割區數目是否與資料行之資料區段對應的分割區數目相符。|檢查區段對應時資料庫一致性檢查 (DBCC) 失敗。|  
|資料行|確認資料行區段中的記錄數目是否與儲存在該資料行區段之索引中的記錄計數相符。|儲存層發生損毀。 '%{parent/}' 資料行中的區段集合已損毀。|  
|資料行|如果資料行沒有區段統計資料，便引發錯誤。|檢查區段統計資料時資料庫一致性檢查 (DBCC) 失敗。|  
|資料行|如果資料行沒有壓縮資訊或區段儲存體，便引發錯誤。|資料庫檔案無法通過一致性檢查。|  
|資料行|如果資料行的區段統計資料與最小資料識別碼、最大資料識別碼、相異值數目、資料列數目或 NULL 值目前狀態的實際資料行值不符，便回報錯誤。|檢查區段統計資料時資料庫一致性檢查 (DBCC) 失敗。|  
|ColumnSegment|如果最小資料識別碼或最大資料識別碼小於系統保留的 NULL 值，便將資料行區段資訊標示為損毀。|檢查區段統計資料時資料庫一致性檢查 (DBCC) 失敗。|  
|ColumnSegment|如果這個區段沒有資料列，資料行的最小和最大資料值應設定為系統保留的 NULL 值。  如果值不是 null，便會引發錯誤。|檢查區段統計資料時資料庫一致性檢查 (DBCC) 失敗。|  
|ColumnSegment|如果資料行具有資料列和至少一個非 null 值，便檢查資料行的最小和最大資料識別碼是否大於系統保留的 NULL 值。|檢查區段統計資料時資料庫一致性檢查 (DBCC) 失敗。|  
|內部|確認存放區 Token 化提示是否已設定，如果存放區已處理，是否有有效的內部資料表指標。  如果存放區未處理，便確認所有指標是否皆為 null。<br />如果不是，則傳回一般 DBCC 錯誤。|資料庫檔案無法通過一致性檢查。|  
|DBCC 資料庫|如果資料庫結構描述沒有任何資料表，或具有一或多個無法存取的資料表，便引發錯誤。|儲存層發生損毀。 '%{parent/}' 資料庫中的資料表集合已損毀。|  
|DBCC 資料庫|如果資料表已標示為暫存或具有未知類型，便引發錯誤。|發現錯誤的資料表類型。|  
|DBCC 資料庫|如果資料表的關聯性數目為負值，抑或是如果資料表具有已定義的關聯性，但找不到對應的關聯性結構時，便引發錯誤。|儲存層發生損毀。 '%{parent/}' 資料表中的關聯性集合已損毀。|  
|DBCC 資料庫|如果資料庫的相容性層級是 1050 (SQL Server 2008 R2 PowerPivot v1.0)，且關聯性數目超過模型中的資料表數目，便將資料庫標示為損毀。|資料庫檔案無法通過一致性檢查。|  
|DBCC 資料表|針對驗證中的資料表，檢查資料行數目是否小於零，如果為 true，便引發錯誤。  如果資料表中資料行的資料行存放區是 NULL，也會引發錯誤。|儲存層發生損毀。 '%{parent/}' 資料表中的資料行集合已損毀。|  
|DBCC 分割區|檢查驗證中之分割區所屬的資料表，如果資料表的資料行數目小於零，表示資料表的資料行集合已損毀。 如果資料表中資料行的資料行存放區是 NULL，也會引發錯誤。|儲存層發生損毀。 '%{parent/}' 資料表中的資料行集合已損毀。|  
|DBCC 分割區|針對選取之分割區的每個資料行執行迴圈，並檢查分割區的每個區段具有資料行區段結構的有效連結。  如果有任何包含 NULL 連結的區段，便將分割區視為損毀。|儲存層發生損毀。 '%{parent/}' 資料行中的區段集合已損毀。|  
|資料行|如果資料行類型不正確，便傳回錯誤。|發現錯誤的區段類型。|  
|資料行|如果任何有資料行之資料行中的區段數目為負數計數，抑或是指向區段之資料行區段結構的指標含有 NULL 連結，便傳回錯誤。|儲存層發生損毀。 '%{parent/}' 資料行中的區段集合已損毀。|  
|DBCC 命令|DBCC 命令在透過 DBCC 作業進行時，將會回報多個狀態訊息。  它會在啟動之前回報狀態訊息，包括資料庫、資料表或物件的資料行名稱，然後在每個物件的檢查完成後再回報一次。|正在檢查的一致性\<objectname > \<objecttype >。 階段︰前置檢查。<br /><br /> 正在檢查的一致性\<objectname > \<objecttype >。 階段︰後置檢查。|  
  
## <a name="common-resolutions-for-error-conditions"></a>解決錯誤狀況的常見方法  
 以下錯誤會出現在 SQL Server Management Studio 或 msmdsrv.log 檔案中。 當有一或多個未通過的檢查時，這些錯誤便會出現。 建議的解決方式是重新處理物件、刪除和重新部署方案或還原資料庫，須視錯誤類型而定。  
  
|錯誤|問題|解決方案|  
|-----------|-----------|----------------|  
|**中繼資料管理員出現錯誤**<br /><br /> 物件參考 '\<objectID >' 無效。 它不符合中繼資料類別階層的結構。|格式不正確的命令|檢查命令語法。 最有可能的情況是您納入了較低層級的物件，卻未指定該物件的一或多個父物件。|  
|**中繼資料管理員出現錯誤**<br /><br /> 任一\<物件 > 識別碼為 '\<objectID >' 不存在於\<parentobject > 識別碼為'\<j >'，或使用者沒有存取物件的權限。|索引損毀 (多維度)|重新處理物件和任何相依的物件。|  
|**在分割區的一致性檢查期間發生錯誤**<br /><br /> 時的一致性檢查，發生錯誤\<分割區名稱 > 的資料分割\<量值群組名稱 > 量值群組\<-n a m > 從 cube \<-n a m > 資料庫。 請重新處理分割區或索引，以修正損毀。|索引損毀 (多維度)|重新處理物件和任何相依的物件。|  
|**分割區區段統計資料已損毀**|索引損毀 (多維度)|重新處理物件和任何相依的物件。|  
|**分割區區段已損毀**|中繼資料損毀 (多維度或表格式)|刪除和重新部署專案，或從備份還原後再重新處理。<br /><br /> 如需相關指示，請參閱 [如何處理 Analysis Services 資料庫中的損毀 (部落格)](http://blogs.msdn.com/b/karang/archive/2010/08/11/how-to-deal-with-corruption-in-analysis-services.aspx) 。|  
|**資料表中繼資料損毀**<br /><br /> 資料表\<資料表名稱 > 中繼資料檔案已損毀。 在 DataFileList 節點下找不到主要資料表。|中繼資料損毀 (僅限表格式)|刪除和重新部署專案，或從備份還原後再重新處理。<br /><br /> 如需相關指示，請參閱 [如何處理 Analysis Services 資料庫中的損毀 (部落格)](http://blogs.msdn.com/b/karang/archive/2010/08/11/how-to-deal-with-corruption-in-analysis-services.aspx) 。|  
|**儲存層發生毀損**<br /><br /> 儲存層發生毀損： 集合\<類型名稱 > 中\<父系名稱 >\<父類型 > 已損毀。|中繼資料損毀 (僅限表格式)|刪除和重新部署專案，或從備份還原後再重新處理。<br /><br /> 如需相關指示，請參閱 [如何處理 Analysis Services 資料庫中的損毀 (部落格)](http://blogs.msdn.com/b/karang/archive/2010/08/11/how-to-deal-with-corruption-in-analysis-services.aspx) 。|  
|**遺漏系統資料表**<br /><br /> 系統資料表\<資料表名稱 > 遺漏。|物件損毀 (僅限表格式)|重新處理物件和任何相依的物件|  
|**資料表統計資料損毀**<br /><br /> 資料表的系統資料表的統計資料\<資料表名稱 > 遺漏。|中繼資料損毀 (僅限表格式)|刪除和重新部署專案，或從備份還原後再重新處理。<br /><br /> 如需相關指示，請參閱 [如何處理 Analysis Services 資料庫中的損毀 (部落格)](http://blogs.msdn.com/b/karang/archive/2010/08/11/how-to-deal-with-corruption-in-analysis-services.aspx) 。|  
  
## <a name="disable-automatic-consistency-checks-on-database-load-operations-through--the-msmdsrvini-configuration-file"></a>透過 msmdsrv.ini 組態檔停用資料庫載入作業的自動一致性檢查  
 雖然我們不建議採用這個方法，不過您可以停用資料庫載入事件發生時自動進行的內建資料庫一致性檢查 (僅限表格式資料庫)。 若要這樣做，您需要修改 msmdsrv.ini 檔案中的組態設定︰  
  
```  
<ConfigurationSettings>  
     <Vertipaq />  
          <DisableConsistencyChecks />  
```  
  
 這項設定不在組態檔中，您必須手動加入。  
  
 下列是有效值：  
  
-   **-2** (預設值) 啟用 DBCC。 如果伺服器能在高確定程度的情況下以邏輯方式解決錯誤，將會自動套用修正程式， 否則會記錄錯誤。  
  
-   **-1** 部分啟用 DBCC。 它可進行 RESTORE 和交易結束時檢查資料庫狀態的認可前驗證。  
  
-   **0** 部分啟用 DBCC。 在 RESTORE、IMAGELOAD、LOCALCUBELOAD 和 ATTACH 作業期間  
         執行資料庫一致性檢查。  
  
-   **1** 停用 DBCC。 停用資料完整性檢查，不過還原序列化檢查仍會發生。  
  
> [!NOTE]  
>  在根據需求執行命令時，這項設定不會對 DBCC 產生任何影響。  
  
## <a name="see-also"></a>另請參閱  
 [處理資料庫、資料表或資料分割 &#40;Analysis Services&#41;](../../analysis-services/tabular-models/process-database-table-or-partition-analysis-services.md)   
 [處理多維度模型 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [監視 Analysis Services 執行個體](../../analysis-services/instances/monitor-an-analysis-services-instance.md)   
 [Analysis Services 中表格式模型的相容性層級](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [Analysis Services 的伺服器屬性](../../analysis-services/server-properties/server-properties-in-analysis-services.md)  
  
  
