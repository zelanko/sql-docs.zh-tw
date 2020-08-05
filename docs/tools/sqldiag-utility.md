---
title: SQLdiag 公用程式
description: 使用 SQLdiag 公用程式從 SQL Server 與其他類型的伺服器收集記錄檔案與資料檔案，並監視伺服器一段時間或針對問題進行疑難排解。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- command prompt utilities [SQL Server], SQLdiag
- stopping diagnostic collection
- storing diagnostic information
- performance [SQL Server], diagnostic collection
- diagnostic records [SQL Server]
- scripts [SQL Server], diagnostic collection
- logs [SQL Server], diagnostic collection
- starting diagnostic collection
- clustered instance of SQL Server
- monitoring performance [SQL Server], diagnostic collection
- security [SQL Server], diagnostic collection
- SQLDIAG service
- space [SQL Server], diagnostic collection
- SQLdiag utility
- disk space [SQL Server], diagnostic collection
- configuration files [SQL Server]
- automatic diagnostic collection
- clusters [SQL Server], diagnostic collection
ms.assetid: 45ba1307-33d1-431e-872c-a6e4556f5ff2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 122aa921cb742d05c46e2d32430c857f4a723dee
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86920894"
---
# <a name="sqldiag-utility"></a>SQLdiag 公用程式
[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]
  **SQLdiag** 公用程式是一種可當做主控台應用程式或服務加以執行的一般用途診斷集合公用程式。 您可以使用 **SQLdiag** ，從 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 和其他類型的伺服器收集記錄檔案和資料檔案，並使用其監視一段時間的伺服器，或對伺服器的特定問題進行疑難排解。 **SQLdiag** 的用途是為了加速及簡化 [!INCLUDE[msCoName](../includes/msconame-md.md)] 客戶支援服務的診斷資訊收集工作。  
  
> [!NOTE]  
>  此公用程式可能會變更，而且依賴其命令列引數或行為的應用程式或指令碼，在未來版本中可能無法正確運作。  
  
 **SQLdiag** 可以收集下列類型的診斷資訊：  
  
-   Windows 效能記錄  
  
-   Windows 事件記錄  
  
-   [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 追蹤  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 封鎖資訊  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 組態資訊  
  
 您可以編輯組態檔 SQLDiag.xml，指定您希望 **SQLdiag** 收集的資訊類型，後續的章節會有相關說明。  
  
## <a name="syntax"></a>語法  
  
```  
  
sqldiag   
     { [/?] }  
     |  
     { [/I configuration_file]  
       [/O output_folder_path]  
       [/P support_folder_path]  
       [/N output_folder_management_option]  
       [/M machine1 [ machine2 machineN]| @machinelistfile]  
       [/C file_compression_type]  
       [/B [+]start_time]  
       [/E [+]stop_time]  
       [/A SQLdiag_application_name]  
       [/T { tcp [ ,port ] | np | lpc } ]  
       [/Q] [/G] [/R] [/U] [/L] [/X] }  
     |  
     { [START | STOP | STOP_ABORT] }  
     |  
     { [START | STOP | STOP_ABORT] /A SQLdiag_application_name }  
```  
  
## <a name="arguments"></a>引數  
 **/?**  
 顯示使用資訊。  
  
 **/I** _configuration_file_  
 設定 **SQLdiag** 要使用的組態檔。 依預設， **/I** 會設為 SQLDiag.Xml。  
  
 **/O** _output_folder_path_  
 將 **SQLdiag** 輸出重新導向至指定的資料夾。 如果未指定 **/O** 選項， **SQLdiag** 輸出會寫入 **SQLdiag** 啟動資料夾之下名稱為 SQLDIAG 的子資料夾中。 如果 [SQLDIAG] 資料夾不存在， **SQLdiag** 會嘗試建立它。  
  
> [!NOTE]  
>  輸出資料夾位置相對於可以使用 **/P**指定的支援資料夾位置。 若要為輸出資料夾設定完全不同的位置，請對 **/O**指定完整的目錄路徑。  
  
 **/P** _support_folder_path_  
 設定支援資料夾路徑。 依預設， **/P** 會設為 **SQLdiag** 可執行檔所在的資料夾。 此支援資料夾包含 **SQLdiag** 支援檔案，例如 XML 組態檔、Transact-SQL 指令碼與公用程式在診斷收集期間所使用的其他檔案。 如果您使用此選項指定替代支援檔案路徑， **SQLdiag** 會將它需要的支援檔案自動複製到指定的資料夾 (如果它們尚不存在)。  
  
> [!NOTE]  
>  若要將目前資料夾設為支援路徑，請在命令列上指定 **%cd%** ，如下所示：  
>   
>  **SQLDIAG /P %cd%**  
  
 **/N** _output_folder_management_option_  
 設定 **SQLdiag** 在啟動時，是要覆寫或重新命名輸出資料夾。 可用選項：  
  
 1 = 覆寫輸出資料夾 (預設值)  
  
 2 = 當 **SQLdiag** 啟動時，它會將輸出資料夾重新命名為 SQLDIAG_00001、SQLDIAG_00002 等。 在重新命名目前的輸出資料夾之後， **SQLdiag** 會將輸出寫入預設輸出資料夾 SQLDIAG 中。  
  
> [!NOTE]  
>  **SQLdiag** 在啟動時不會將輸出附加至目前的輸出資料夾。 它只能覆寫預設輸出資料夾 (選項 1)，或重新命名資料夾 (選項 2)，然後將輸出寫入新的預設輸出資料夾 SQLDIAG 中。  
  
 **/M** _machine1_ [ *machine2* *machineN*] | *\@machinelistfile*  
 覆寫組態檔中指定的電腦。 依預設，組態檔是 SQLDiag.Xml，或是以 **/I** 參數來設定。 當指定一部以上的電腦時，請用空格隔開每一個電腦名稱。  
  
 使用 *\@machinelistfile* 指定要儲存在組態檔中的電腦清單檔案名稱。  
  
 **/C** _file_compression_type_  
 設定 **SQLdiag** 輸出資料夾檔案所用的檔案壓縮類型。 可用選項：  
  
 0 = 無 (預設值)  
  
 1 = 使用 NTFS 壓縮  
  
 **/B** [ **+** ]*start_time*  
 依照下列格式來指定開始收集診斷資料的日期和時間：  
  
 YYYYMMDD_HH:MM:SS  
  
 時間使用 24 小時標記法指定。 例如，下午 2:00 應該指定為 **14:00:00**。  
  
 請利用 **+** (不含日期 (只有 HH:MM:SS)) 來指定相對於目前日期和時間的時間。 例如，如果您指定 **/B +02:00:00**， **SQLdiag** 會等候 2 小時，再開始收集資訊。  
  
 請勿在 **+** 和指定的 *start_time*之間插入空格。  
  
 如果您指定的開始時間已經過去， **SQLdiag** 會強制變更開始日期，使開始日期和時間設定在未來。 例如，如果您指定 **/B 01:00:00** ，且目前的時間是 08:00:00， **SQLdiag** 會強制變更開始日期，使開始日期設定在隔天。  
  
 請注意， **SQLdiag** 會使用執行公用程式之電腦的本機時間。  
  
 **/E** [ **+** ]*stop_time*  
 依照下列格式來指定停止收集診斷資料的日期和時間：  
  
 YYYYMMDD_HH:MM:SS  
  
 時間使用 24 小時標記法指定。 例如，下午 2:00 應該指定為 **14:00:00**。  
  
 請利用 **+** (不含日期 (只有 HH:MM:SS)) 來指定相對於目前日期和時間的時間。 例如，如果您利用 **/B +02:00:00 /E +03:00:00**來指定開始時間和結束時間， **SQLdiag** 會等候 2 小時再開始收集資訊，之後會收集 3 小時的資訊，再停止並結束。 如果未指定 **/B** ， **SQLdiag** 會立即開始收集診斷資訊，並會在 **/E**所指定的日期和時間結束。  
  
 請勿在 **+** 和指定的 *start_time* 或 *end_time*之間插入空格。  
  
 請注意， **SQLdiag** 會使用執行公用程式之電腦的本機時間。  
  
 **/A**  _SQLdiag_application_name_  
 使 **SQLdiag** 公用程式的多個執行個體可以針對相同的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體執行。  
  
 每一個 *SQLdiag_application_name* 會識別一個不同的 **SQLdiag**執行個體。 *SQLdiag_application_name* 執行個體和 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體名稱之間沒有關聯性。  
  
 *SQLdiag_application_name* 可用來啟動或停止 **SQLdiag** 服務的特定執行個體。  
  
 例如：  
  
 **SQLDIAG START /A**  _SQLdiag_application_name_  
  
 它也可以與 **/R** 選項一起使用，將 **SQLdiag** 的特定執行個體註冊為服務。 例如：  
  
 **SQLDIAG /R /A** _SQLdiag_application_name_  
  
> [!NOTE]  
>  **SQLdiag** 會自動將 DIAG$ 前置於為 *SQLdiag_application_name*所指定的執行個體名稱。 其可為在您將 **SQLdiag** 註冊成服務時，提供實用的服務名稱。  
  
 /T { tcp [ ,*port* ] | np | lpc }  
 使用指定的通訊協定連接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體。  
  
 tcp [,*port*]  
 傳輸控制通訊協定/網際網路通訊協定 (TCP/IP)。 您可以選擇性地為此連接指定通訊埠編號。  
  
 np  
 具名管道。 根據預設， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的預設執行個體會針對具名執行個體接聽具名管道 `\\.\pipe\sql\query` 和 `\\.\pipe\MSSQL$<instancename>\sql\query` 。 您無法使用替代管道名稱來連接 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體。  
  
 lpc  
 本機程序呼叫。 如果用戶端連接到同一部電腦上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體，也可以使用此共用的記憶體通訊協定。  
  
 **/Q**  
 以安靜模式執行 **SQLdiag** 。 **/Q** 會抑制所有提示，如密碼提示。  
  
 **/G**  
 以一般模式執行 **SQLdiag** 。 指定 **/G** 之後，在啟動時， **SQLdiag** 就不會強制執行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 連線檢查，或確認使用者是否為 **系統管理員** 固定伺服器角色的成員。 但是， **SQLdiag** 會延遲 Windows 判斷使用者是否具有適當的權限，以收集各項要求的診斷。  
  
 如果未指定 **/G** ， **SQLdiag** 會檢查並判斷使用者是否為 Windows **Administrator** 群組的成員，如果使用者不是 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Administrator **群組成員，則不會收集** 診斷資訊。  
  
 **/R**  
 將 **SQLdiag** 註冊為服務。 您將 **SQLdiag** 註冊成服務時所指定的任何命令列引數都會保留下來，以便之後執行這項服務時使用。  
  
 當 **SQLdiag** 註冊為服務時，預設服務名稱為 SQLDIAG。 您可以使用 **/A** 引數變更服務名稱。  
  
 使用 **START** 命令列引數來啟動服務：  
  
 **SQLDIAG START**  
  
 您也可以使用 **net start** 命令來啟動服務：  
  
 **net  start SQLDIAG**  
  
 **/U**  
 將 **SQLdiag** 取消註冊為服務。  
  
 若要取消註冊具名 **SQLdiag** 執行個體，也請使用 **/A** 引數。  
  
 **/L**  
 若也分別以 **/B** 或 **/E** 引數指定開始時間或結束時間，請在連續模式下執行 **SQLdiag** 。 當因為排程關閉而停止收集診斷資訊之後，會自動重新啟動**SQLdiag** 。 例如，透過使用 **/E** 或 **/X** 引數。  
  
> [!NOTE]  
>  如果開始時間或結束時間不是使用**SQLdiag** 和 **/L** 命令列引數指定，則 **SQLdiag** 會忽略 **/L** comm會忽略 line arguments.  
  
 使用 **/L** 不代表服務模式。 將 **SQLdiag** 執行為服務時若要使用 **/L** ，請在註冊服務時於命令列上指定。  
  
 **/X**  
 以快照集模式執行 **SQLdiag** 。 **SQLdiag** 會取得所有所設定之診斷資訊的快照，再自動關閉。  
  
 **START** | **STOP** | **STOP_ABORT**  
 啟動或停止 **SQLdiag** 服務。 **STOP_ABORT** 會在未完成它目前正在收集的診斷資訊收集工作的情況下，強制盡快關閉。  
  
 使用這些服務控制引數時，它們必須是命令列所使用的第一個引數。 例如：  
  
 **SQLDIAG START**  
  
 只有指定 **SQLdiag** 具名執行個體的 **/A**引數，才可以與 **START**、 **STOP**或 **STOP_ABORT** 一起使用，來控制 **SQLdiag** 服務的特定執行個體。 例如：  
  
 **SQLDIAG START /A** _SQLdiag_application_name_  
  
## <a name="security-requirements"></a>安全性需求  
 除非 **SQLdiag** 於一般模式下執行 (藉由指定 **/G** 命令列引數)，否則執行 **SQLdiag** 的使用者必須是 Windows **Administrator** 群組成員，以及 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] **系統管理員** 固定伺服器角色的成員。 依預設， **SQLdiag** 會使用 Windows 驗證來連接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ，但它也支援 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證。  
  
## <a name="performance-considerations"></a>效能考量  
 執行 **SQLdiag** 的效能結果，會隨著您設定它要收集的診斷資料類型而不同。 例如，如果您已設定 **SQLdiag** 會收集 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 追蹤資訊，則您選擇要追蹤的事件類別愈多，伺服器效能受到的影響就愈大。  
  
 執行 **SQLdiag** 的效能影響大約相當於個別收集已設定之診斷資訊的成本總和。 例如，利用 **SQLdiag** 收集追蹤，其帶來的效能成本與利用 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]收集是一樣的。 使用 **SQLdiag** 所造成的效能影響可不予理會。  
  
## <a name="required-disk-space"></a>所需磁碟空間  
 由於 **SQLdiag** 可以收集不同類型的診斷資訊；因此，執行 **SQLdiag** 所需要的可用磁碟空間也各不相同。 收集的診斷資訊數量會隨著伺服器所處理之工作負載的本質和數量而不同，範圍可能在幾 MB 到幾 GB 之間。  
  
## <a name="configuration-files"></a>組態檔  
 在啟動時， **SQLdiag** 會讀取組態檔及已指定的命令列引數。 您可以在組態檔中指定 **SQLdiag** 所要收集的診斷資訊類型。 依預設， **SQLdiag** 會使用 SQLDiag.Xml 組態檔，此組態檔會在每次執行此工具時加以擷取，且其位於 **SQLdiag** 公用程式啟動資料夾中。 組態檔會使用 XML 結構描述 SQLDiag_schema.xsd，此結構描述也會在每次執行 **SQLdiag** 時，從可執行檔直接擷取到公用程式啟動目錄中。  
  
### <a name="editing-the-configuration-files"></a>編輯組態檔  
 您可以複製和編輯 SQLDiag.Xml 來變更 **SQLdiag** 所收集的診斷資料類型。 編輯組態檔時，請務必使用可驗證組態檔之 XML 結構描述的 XML 編輯器，例如 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]。 您不應該直接編輯 SQLDiag.Xml。 但是，您應該複製一份 SQLDiag.Xml，然後在相同資料夾中，將它重新命名成新的檔案名稱。 接著，請編輯新的檔案，再利用 **/I** 引數，將它傳遞給 **SQLdiag**。  
  
#### <a name="editing-the-configuration-file-when-sqldiag-runs-as-a-service"></a>在 SQLdiag 執行為服務時編輯組態檔  
 如果您已將 **SQLdiag** 執行為服務，且需要編輯組態檔，請指定 **/U** 命令列引數取消註冊 SQLDIAG 服務，再利用 **/R** 命令列引數重新註冊這項服務。 取消登錄這項服務後再重新登錄它，會移除 Windows 登錄中快取的舊組態資訊。  
  
## <a name="output-folder"></a>輸出資料夾  
 如果您沒有利用 **/O** 引數指定輸出資料夾， **SQLdiag** 會在 **SQLdiag** 啟動資料夾之下，建立名稱為 SQLDIAG 的子資料夾。 對於需要大量追蹤的診斷資訊收集 (例如 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] )，請確定輸出資料夾位於擁有足夠空間，可以儲存所要求之診斷輸出的本機磁碟機上。  
  
 當 **SQLdiag** 重新啟動時，它會覆寫輸出資料夾的內容。 若要避免發生此情形，請在命令列上指定 **/N 2** 。  
  
## <a name="data-collection-process"></a>資料收集程序  
 當 **SQLdiag** 啟動時，它會執行收集 SQLDiag.Xml 中所指定之診斷資料所需的初始化檢查。 這個程序可能需要幾秒鐘。 當以主控台應用程式執行 **SQLdiag** 時，在它開始收集診斷資料之後，會出現一則訊息，通知您 **SQLdiag** 收集作業已經開始，您可以按 CTRL+C 加以停止。 當 **SQLdiag** 執行為服務時，會在 Windows 事件記錄檔中寫入一則類似的訊息。  
  
 如果您利用 **SQLdiag** 診斷可以重現的問題，請等到收到這則訊息之後，再於伺服器中重現此問題。  
  
 **SQLdiag** 會以平行方式收集大部分的診斷資料。 除了從 Windows 效能記錄檔和事件記錄檔收集資訊之外，所有診斷資訊都是藉由連線到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] **sqlcmd** 公用程式或 Windows 命令處理器之類的工具加以收集。 **SQLdiag** 會在每部電腦上各使用一個工作者執行緒，監視這些其他工具的診斷資料收集，通常會同時等待多個工具完成。 在收集過程期間， **SQLdiag** 會將每一個診斷的輸出路由傳送至輸出資料夾。  
  
## <a name="stopping-data-collection"></a>停止收集資料  
 在 **SQLdiag** 開始收集診斷資料之後，除非您將它停止，或將它設定成在指定的時間停止，否則它會持續作業。 您可以利用可讓您指定停止時間的 **/E** 引數，或利用使 **SQLdiag** 以快照集模式執行的 **/X** 引數，將 **SQLdiag** 設定成於指定的時間停止。  
  
 當 **SQLdiag** 停止時，它會停止所有已啟動的診斷作業。 例如，它會停止正在收集的 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 追蹤、停止執行正在執行的 [!INCLUDE[tsql](../includes/tsql-md.md)] 指令碼，以及停止在資料收集期間繁衍的任何子程序。 診斷資料收集完成之後， **SQLdiag** 便會結束。  
  
> [!NOTE]  
>  不支援暫停 **SQLdiag** 服務。 如果您嘗試暫停 **SQLdiag** 服務，它會將您暫停它時正在收集的診斷收集完成之後才停止。 如果您在停止 **SQLdiag** 之後又重新加以啟動，則該應用程式會重新啟動並覆寫輸出資料夾。 若要避免覆寫輸出資料夾，請在命令列上指定 **/N 2** 。  
  
 **停止當做主控台應用程式執行的 SQLdiag**  
  
 如果您將 **SQLdiag** 執行為主控台應用程式，在執行 **SQLdiag** 的主控台視窗中，按 CTRL+C 可加以停止。 按 CTRL+C 之後，主控台視窗中會出現一則訊息，通知您 **SQLDiag** 的資料收集即將結束，您應該等候該處理序關閉，這可能需要幾分鐘的時間。  
  
 按 Ctrl+C 兩次結束所有子診斷程序，並立即結束應用程式。  
  
 **停止執行為服務的 SQLdiag**  
  
 如果您將 **SQLdiag** 執行為服務，請在 **SQLdiag** 啟動資料夾內執行 **SQLDiag STOP** 加以停止。  
  
 如果您在相同的電腦上執行多個 **SQLdiag** 執行個體，則當您停止服務時，也可以在命令列上傳遞 **SQLdiag** 執行個體名稱。 例如，若要停止 **SQLdiag** 執行個體 Instance1，請使用下列語法：  
  
```  
SQLDIAG STOP /A Instance1  
```  
  
> [!NOTE]  
>  **/A** 是唯一可以與 **START**、 **STOP**或 **STOP_ABORT**一起使用的命令列引數。 如果您需要以其中一個服務控制動詞指定 **SQLdiag** 的具名執行個體，請在命令列上該控制動詞後指定 **/A** ，如上述語法範例所示。 使用控制動詞時，它們必須是命令列上的第一個引數。  
  
 若要盡快停止服務，請執行公用程式啟動資料夾中的 **SQLDIAG STOP_ABORT** 。 此命令會中止目前正在執行的任何診斷收集，而不會等到它們完成。  
  
> [!NOTE]  
>  請使用 **SQLDiag STOP** 或 **SQLDIAG STOP_ABORT** 停止 **SQLdiag** 服務。 請勿使用 Windows 服務主控台停止 **SQLdiag** 或其他 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 服務。  
  
## <a name="automatically-starting-and-stopping-sqldiag"></a>自動啟動和停止 SQLdiag  
 若要在指定時間自動啟動及停止診斷資料收集，請使用 **/B**_start\_time_ 和 **/E**_stop\_time_ 引數，並採用 24 小時制標記法。 例如，如果您要針對大約在 02:00:00 一致出現的問題進行疑難排解，您可以將 **SQLdiag** 設定成在 01:00 自動開始收集診斷資料且在 03:00:00 自動停止。 請利用 **/B** 和 **/E** 引數來指定開始和停止時間。 請利用 24 小時標記法來指定開始和停止的確切日期和時間，格式為 YYYYMMDD_HH:MM:SS。 若要指定相對的開始或停止時間，請依照下列範例所示，在開始和停止時間之前附加 **+** ，並省略日期部分 (YYYYMMDD_)，如此會讓 **SQLdiag** 等候 1 小時再開始收集資訊，之後會收集 3 小時的資訊，再停止並結束：  
  
```  
sqldiag /B +01:00:00 /E +03:00:00  
```  
  
 指定相對的 *start_time* 之後， **SQLdiag** 就會在相對於目前日期和時間的時間啟動。 指定相對的 *end_time* 之後， **SQLdiag** 就會在相對於指定的 *start_time*的時間結束。 如果您指定的開始或結束日期和時間已經過去， **SQLdiag** 會強制變更開始日期，讓開始日期和時間設定在未來。  
  
 對您選擇的開始和結束日期而言，這有重要的影響。 請考慮下列範例：  
  
```  
sqldiag /B +01:00:00 /E 08:30:00  
```  
  
 如果目前的時間是 08:00，在實際開始收集診斷資訊之前，結束時間便已過去。 因為 **SQLDiag** 會將發生在過去的開始和結束日期自動調整至隔天，所以在此範例中，診斷收集會從今天 09:00 開始 (已使用 **+** 指定相對的開始時間)，並繼續收集直到隔天早上 08:30。  
  
### <a name="stopping-and-restarting-sqldiag-to-collect-daily-diagnostics"></a>停止和重新啟動 SQLdiag 來收集每天的診斷資訊  
 若要每天收集一組指定的診斷資訊，而不要手動啟動和停止 **SQLdiag**，請使用 **/L** 引數。 **/L** 引數會在排程的關閉之後，自行重新啟動以持續執行 **SQLdiag** 。 若指定 **/L** ，且 **SQLdiag** 因為達到使用 **/E** 引數所指定的結束時間而停止，或因為使用 **/X** 引數以快照集模式執行而停止， **SQLdiag** 都將會重新啟動而不是結束。  
  
 下列範例指定以連續模式執行 **SQLdiag** ，以便在 03:00:00 和 05:00:00 之間收集診斷資料之後，自動重新啟動。  
  
```  
sqldiag /B 03:00:00 /E 05:00:00 /L  
```  
  
 下列範例指定以連續模式執行 **SQLdiag** ，以在 03:00:00 時取得診斷資料快照集之後，自動重新啟動。  
  
```  
sqldiag /B 03:00:00 /X /L  
```  
  
## <a name="running-sqldiag-as-a-service"></a>將 SQLdiag 執行為服務  
 當您要利用 **SQLdiag** 長時間收集診斷資料，且在這段時間中您可能需要登出執行 **SQLdiag** 的電腦，您可以將其執行為服務。  
  
 **將 SQLDiag 註冊執行為服務**  
  
 您可以在命令列處指定 **/R** 引數，將 **SQLdiag** 註冊為以服務方式執行。 這會將 **SQLdiag** 註冊執行為服務 **SQLdiag** 服務名稱是 SQLDIAG。 當您將 **SQLDiag** 註冊成服務時，您在命令列上指定的所有其他引數都會保留下來，啟動這項服務時會重複使用它們。  
  
 若要變更預設 SQLDIAG 服務名稱，請使用 **/A** 命令列引數來指定另一個名稱。 **SQLdiag** 會將 DIAG$ 自動前置於任何以 **/A** 指定的 **SQLdiag** 執行個體名稱，以建立實用的服務名稱。  
  
 **若要取消登錄 SQLDIAG 服務**  
  
 若要取消註冊服務，請指定 **/U** 引數。 取消註冊 **SQLdiag** 的服務身分，也會刪除該服務的 Windows 登錄機碼。  
  
 **若要啟動或重新啟動 SQLDIAG 服務**  
  
 若要啟動或重新啟動 SQLDIAG 服務，請從命令列執行 **SQLDiag START** 。  
  
 如果您使用 **/A** 引數執行多個 **SQLdiag** 的執行個體，當您啟動服務時，您也可以在命令列上傳遞 **SQLdiag** 執行個體名稱。 例如，若要開始 **SQLdiag** 執行個體 Instance1，請使用下列語法：  
  
```  
SQLDIAG START /A Instance1  
```  
  
 您也可以利用 **net start** 命令來啟動 SQLDIAG 服務。  
  
 當您重新啟動 **SQLdiag**時，它會覆寫目前輸出資料夾的內容。 為避免發生此情形，請在命令列上指定 **/N 2** ，在公用程式啟動時重新命名輸出資料夾。  
  
 不支援暫停 **SQLdiag** 服務。  
  
## <a name="running-multiple-instances-of-sqldiag"></a>執行 SQLdiag 的多個執行個體  
 在相同電腦的命令列上指定 **/A**_SQLdiag\_application\_name_ 來執行多個 **SQLdiag** 的執行個體。 這對於同時從相同 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體收集不同的診斷集很有幫助。 例如，您可以設定 **SQLdiag** 的具名執行個體，持續執行輕量型資料收集。 之後，如果 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]上發生特定的問題，您可以執行預設的 **SQLdiag** 執行個體來收集該問題的診斷資訊，或蒐集 [!INCLUDE[msCoName](../includes/msconame-md.md)] 客戶支援服務要求您搜尋的一組診斷來診斷問題。  
  
## <a name="collecting-diagnostic-data-from-clustered-sql-server-instances"></a>從叢集 SQL Server 執行個體收集診斷資料  
 **SQLdiag** 支援從叢集的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體中收集診斷資料。 若要從叢集的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體收集診斷資料，請確定已在設定檔 SQLDiag.Xml 中，為 **\<Machine>** 元素的 **name** 屬性指定 **"."** ，而且不要在命令列上指定 **/G** 引數。 預設會在組態檔中對 **name** 屬性指定 **"."** ，且會關閉 **/G** 引數。 通常，從叢集的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體中收集時，您不需要編輯組態檔或變更命令列引數。  
  
 當 **"."** 指定為機器名稱時， **SQLdiag** 會偵測到它執行於叢集上，同時會從安裝在叢集上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的所有虛擬執行個體，擷取診斷資訊。 如果您只想要從電腦上執行的一個 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 虛擬執行個體收集診斷資訊，請在 SQLDiag.Xml 中，為 **\<Machine>** 元素的 **name** 屬性指定該虛擬 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。  
  
> [!NOTE]  
>  若要從叢集的 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 執行個體收集 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 追蹤資訊，必須在叢集上啟用管理共用 (ADMIN$)。  
  
## <a name="see-also"></a>另請參閱  
 [命令提示字元公用程式參考 &#40;Database Engine&#41;](../tools/command-prompt-utility-reference-database-engine.md)  
  
  
