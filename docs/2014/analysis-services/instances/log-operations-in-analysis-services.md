---
title: 記錄在 Analysis Services 中的作業 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: aa1db060-95dc-4198-8aeb-cffdda44b140
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 58169ffcc696c87addee0417700ba131a71e12f0
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53363750"
---
# <a name="log-operations-in-analysis-services"></a>Analysis Services 中的記錄作業
  Analysis Services 執行個體將會記錄伺服器通知、 錯誤和警告至 msmdsrv.log 檔案-一個用於您所安裝的每個執行個體。 管理員可以參考此記錄檔，獲得例行和異常等事件的深入見解。 最新版本的記錄功能已經過增強，可以加入更多資訊。 記錄檔記錄現在包含產品版本和版本資訊，以及處理器、記憶體、連接及封鎖事件。 您可以在 [記錄改進](https://support.microsoft.com/kb/2965035)檢閱整個變更清單。  
  
 除了內建的記錄功能，許多管理員和開發人員也使用 Analysis Services 社群所提供的工具來收集有關伺服器作業 (例如 **ASTrace**) 的資料。 請參閱[Microsoft SQL Server 社群範例：Analysis Services](https://sqlsrvanalysissrvcs.codeplex.com/)取得下載連結。  
  
 本主題包含下列幾節：  
  
-   [記錄檔的位置和類型](#bkmk_location)  
  
-   [記錄檔組態設定的一般資訊](#bkmk_general)  
  
-   [MSMDSRV 服務記錄檔](#bkmk_msmdsrv)  
  
-   [查詢記錄](#bkmk_querylog)  
  
-   [迷你傾印 (.mdmp) 檔案](#bkmk_mdmp)  
  
-   [秘訣和最佳作法](#bkmk_tips)  
  
> [!NOTE]  
>  如果您正在尋找記錄的相關資訊，您也可能想要追蹤顯示處理和查詢執行路徑的作業。 臨機操作和持續性追蹤 (例如稽核 Cube 存取) 的追蹤物件，以及如何充分運用可以在此頁面上找到連結的 Flight Recorder、SQL Server Profiler 和 xEvents 的建議：[監視 Analysis Services 執行個體](monitor-an-analysis-services-instance.md)。  
  
##  <a name="bkmk_location"></a> 記錄檔的位置和類型  
 Analysis Services 提供如下所述的記錄檔。  
  
|檔案名稱或位置|類型|用於|依預設開啟|  
|---------------------------|----------|--------------|-------------------|  
|Msmdsrv.log|錯誤記錄檔|例行監視和基本疑難排解|是|  
|關聯式資料庫中的 OlapQueryLog 資料表|查詢記錄|收集使用方式的最佳化精靈的輸入|否|  
|Sqldmp<guid\<guid >.mdmp 檔|當機和例外狀況|深入疑難排解|否|  
  
 我們強烈建議使用下列連結，以取得本主題中未涵蓋的其他資訊資源：[初始資料收集提示，Microsoft 支援服務](https://blogs.msdn.com/b/as_emea/archive/2012/01/02/initial-data-collection-for-troubleshooting-analysis-services-issues.aspx)。  
  
##  <a name="bkmk_general"></a> 記錄檔組態設定的一般資訊  
 您可以在 msmdsrv.ini 伺服器組態檔案中找到每個記錄檔的區段，其位於 \Program Files\Microsoft SQL Server\MSAS12.MSSQLSERVER\OLAP\Config 資料夾。 如需編輯此檔案的指示，請參閱 [Configure Server Properties in Analysis Services](../server-properties/server-properties-in-analysis-services.md) 。  
  
 如果可行，我們建議您在 Management Studio 的伺服器屬性頁面中設定記錄屬性。 不過在某些情況下，您必須直接編輯 msmdsrv.ini 檔案，以設定系統管理工具中看不到的設定。  
  
 ![顯示記錄檔設定的組態檔區段](../media/ssas-logfilesettings.png "顯示記錄檔設定的組態檔區段")  
  
##  <a name="bkmk_msmdsrv"></a> MSMDSRV 服務記錄檔  
 Analysis Services 會將伺服器作業記錄至 msmdsrv.log 檔案，其位於 \program files\Microsoft SQL Server\\<執行個體\>\Olap\Log，每個執行個體一個。  
  
 這個記錄檔會在每次服務重新啟動時清空。 在舊版中，管理員之所以重新啟動服務，有時只是為了在記錄檔成長到太大而變得無法使用之前加以清除。 現已不再需要這麼做。 SQL Server 2012 SP2 中及更新版本中推出的組態設定，可讓您控制記錄檔和其歷程記錄的大小：  
  
-   `MaxFileSizeMB` 指定最大記錄檔大小 (以 MB 為單位)。 預設值是 256。 有效的取代值必須是正整數。 達到 `MaxFileSizeMB` 時，Analysis Services 會將目前的檔案重新命名為 msmdsrv{current timestamp}.log 檔案，並啟動新的 msmdsrv.log 檔案。  
  
-   `MaxNumberFiles` 指定保留的較舊的記錄檔。 預設值是 0 (停用)。 您可以將它變更為正整數，以保留記錄檔的版本。 達到 `MaxNumberFiles` 時，Analysis Services 會刪除其名稱中具有最舊的時間戳記的檔案。  
  
 若要使用這些設定，請執行下列動作：  
  
1.  在記事本中開啟 msmdsrv.ini。  
  
2.  複製下列兩行：  
  
    ```  
    <MaxFileSizeMB>256</MaxFileSizeMB>  
    <MaxNumberOfLogFiles>5</MaxNumberOfLogFiles>  
    ```  
  
3.  將兩行貼到 msmdsrv.ini 的的 Log 區段，位於 msmdsrv.log 檔案名稱下。 這兩個設定必須手動加入。 msmdsrv.ini 檔案中沒有其預留位置。  
  
     已變更的組態檔看起來應該如下所示：  
  
    ```  
    <Log>  
    <File>msmdsrv.log</File>  
    <MaxFileSizeMB>256</MaxFileSizeMB>  
    <MaxNumberOfLogFiles>5</MaxNumberOfLogFiles>  
    <FileBufferSize>0</FileBufferSize>  
  
    ```  
  
4.  如果提供的值與您想要的不同，請編輯值。  
  
5.  儲存檔案。  
  
6.  重新啟動服務。  
  
##  <a name="bkmk_querylog"></a> 查詢記錄  
 查詢記錄的名稱與它的功能有些出入，因為它並不會為您記錄使用者的 MDX 或 DAX 查詢活動。 相反地，它會收集 Analysis Services 產生的查詢中的資料，這後續會做為使用方式的最佳化精靈中的資料輸入。 查詢記錄中收集的資料不適合直接分析。 具體而言，資料集是以位元陣列描述，具有零或一，指出查詢中包含的資料集部分。 重申，此資料專供精靈使用。  
  
 針對查詢監視和疑難排解，許多開發人員和管理員會使用社群工具 **ASTrace**來監視查詢。 您也可以使用 SQL Server Profiler、xEvents 或 Analysis Services 追蹤。 請參閱 [監視 Analysis Services 執行個體](monitor-an-analysis-services-instance.md) ，以取得追蹤的相關連結。  
  
 何時應該使用查詢記錄？ 我們建議您在包含使用方式的最佳化精靈的查詢效能微調練習中啟用查詢記錄。 在您啟用功能、建立資料結構以支援它，並設定 Analysis Services 用來找出並填入記錄檔的屬性之前，查詢記錄不會存在。  
  
 若要啟用查詢記錄，請遵循下列步驟：  
  
1.  建立 SQL Server 關聯式資料庫來儲存查詢記錄。  
  
2.  授與 Analysis Services 服務帳戶資料庫的足夠權限。 帳戶需要建立資料表、寫入資料表，並從資料表讀取的權限。  
  
3.  在 SQL Server Management Studio 中，以滑鼠右鍵按一下 **[Analysis Services]** | **[屬性]** | **[一般]**，並將 **CreateQueryLogTable** 設為 true。  
  
4.  如果您想要以不同的速率對查詢取樣，或使用不同的資料表名稱，請選擇性地變更 **QueryLogSampling** 或 **QueryLogTableName** 。  
  
 在您執行足夠的 MDX 查詢以符合取樣需求之前，將不會建立查詢記錄資料表。 比方說，如果您保留預設值 10，您必須先執行至少 10 個查詢，才會建立資料表。  
  
 查詢記錄設定是以整個伺服器為範圍。 您指定的設定會用於此伺服器上執行的所有資料庫。  
  
 ![查詢記錄檔設定，在 Management Studio](../media/ssas-querylogsettings.png "在 Management Studio 中的查詢記錄設定")  
  
 在指定組態設定之後，執行 MDX 查詢多次。 如果取樣設為 10，則執行查詢 11 次。確認已建立資料表。 在 Management Studio 中，連接到關聯式資料庫引擎，開啟資料庫資料夾，開啟 **[資料表]** 資料夾，並確認 **OlapQueryLog** 存在。 如果無法立即看到資料表，請重新整理資料夾，以收取其內容的任何變更。  
  
 允許查詢記錄對使用方式的最佳化精靈累積足夠的資料。 如果查詢量會循環，請擷取足夠的流量來取得具有代表性的資料集。 請參閱 [使用方式的最佳化精靈](https://msdn.microsoft.com/library/ms189706.aspx) ，以取得如何執行此精靈的指示。  
  
 請參閱 [設定 Analysis Services 查詢記錄](https://technet.microsoft.com/library/Cc917676) ，以深入了解查詢記錄組態。 雖然本文件相當老舊，但最新版本中並未變更查詢記錄組態，因此其內含的資訊仍適用。  
  
##  <a name="bkmk_mdmp"></a> 迷你傾印 (.mdmp) 檔案  
 傾印檔案會擷取用於分析異常事件的資料。 Analysis Services 會自動產生迷你傾印 (.mdmp)，以回應伺服器當機、例外狀況，以及一些組態錯誤。 此功能已啟用，但不會自動傳送當機報告。  
  
 當機報告是透過 Msmdsrv.ini 檔案中的 Exception 區段設定。 這些設定會控制記憶體傾印檔案產生。 下列程式碼片段會顯示預設值：  
  
```  
<Exception>  
<CreateAndSendCrashReports>1</CreateAndSendCrashReports>  
<CrashReportsFolder/>  
<SQLDumperFlagsOn>0x0</SQLDumperFlagsOn>  
<SQLDumperFlagsOff>0x0</SQLDumperFlagsOff>  
<MiniDumpFlagsOn>0x0</MiniDumpFlagsOn>  
<MiniDumpFlagsOff>0x0</MiniDumpFlagsOff>  
<MinidumpErrorList>0xC1000000, 0xC1000001, 0xC102003F, 0xC1360054, 0xC1360055</MinidumpErrorList>  
<ExceptionHandlingMode>0</ExceptionHandlingMode>  
<CriticalErrorHandling>1</CriticalErrorHandling>  
<MaxExceptions>500</MaxExceptions>  
<MaxDuplicateDumps>1</MaxDuplicateDumps>  
</Exception>  
```  
  
 **設定當機報告**  
  
 除非 Microsoft 支援另有指示，否則大部分的管理員均會使用預設設定。 這個較舊的知識庫文件仍然用來提供有關如何設定傾印檔案的指示：[如何設定 Analysis Services 以產生記憶體傾印檔案](https://support.microsoft.com/kb/919711)。  
  
 最有可能遭到修改的組態設定是用來判斷是否會產生記憶體傾印檔案的 `CreateAndSendCrashReports` 設定。  
  
|值|描述|  
|-----------|-----------------|  
|0|關閉記憶體傾印檔案。 將會忽略 Exception 區段下的所有其他設定。|  
|1|(預設值) 啟用，但不會傳送記憶體傾印檔案。|  
|2|啟用並自動傳送錯誤報告給 Microsoft。|  
  
 `CrashReportsFolder` 是將傾印檔案的位置。 根據預設，可以在 \Olap\Log 資料夾中找到一個 .mdmp 檔以及相關聯的記錄檔記錄。  
  
 `SQLDumperFlagsOn` 用來產生完整傾印。 根據預設，不會啟用完整傾印。 您可以將此屬性設定為 `0x34`。  
  
 下列連結提供更多背景：  
  
-   [想要使用小型傾印更深入了解 SQL Server](https://blogs.msdn.com/b/sqlcat/archive/2009/09/11/looking-deeper-into-sql-server-using-minidumps.aspx)  
  
-   [如何建立使用者模式傾印檔案](https://support.microsoft.com/kb/931673)  
  
-   [如何使用 Sqldumper.exe 公用程式，在 SQL Server 產生傾印檔案](https://support.microsoft.com/kb/917825)  
  
##  <a name="bkmk_tips"></a> 秘訣和最佳作法  
 本節是整篇文章所述秘訣的回顧。  
  
-   設定 msmdsrv.log 檔案來控制 msmdsrv 記錄檔的大小和數目。 預設不會啟用此設定，因此務必將它們加入做為後續安裝步驟。 請參閱本主題的 [MSMDSRV 服務記錄檔](#bkmk_msmdsrv) 。  
  
-   檢閱來自 Microsoft 客戶支援的這些部落格文章，以了解他們用何資源來取得有關伺服器作業的資訊：[初始資料收集](https://blogs.msdn.com/b/as_emea/archive/2012/01/02/initial-data-collection-for-troubleshooting-analysis-services-issues.aspx)  
  
-   若要找出查詢 Cube 的對象，請使用 ASTrace2012，而不是查詢記錄。 查詢記錄通常用來對使用方式的最佳化精靈提供輸入，其擷取的資料並不易閱讀或解譯。 ASTrace2012 是廣泛使用的社群工具，可擷取查詢作業。 請參閱[Microsoft SQL Server 社群範例：Analysis Services](https://sqlsrvanalysissrvcs.codeplex.com/)。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 執行個體管理](analysis-services-instance-management.md)   
 [使用 SQL Server Profiler 監視 Analysis Services 簡介](introduction-to-monitoring-analysis-services-with-sql-server-profiler.md)   
 [Analysis Services 中設定伺服器屬性](../server-properties/server-properties-in-analysis-services.md)  
  
  
