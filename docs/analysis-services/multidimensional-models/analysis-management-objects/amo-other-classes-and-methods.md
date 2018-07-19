---
title: AMO 其他類別和方法 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: amo
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d77d216ae3390162221e8808fc6047d5c9c35e13
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34024715"
---
# <a name="amo-other-classes-and-methods"></a>AMO 其他類別和方法
  本節包含一般類別不是 OLAP 或資料採礦特有以及屬於管理或管理中的物件時很有幫助[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。 這些類別涵蓋如預存程序、追蹤、例外狀況以及備份與還原等功能。  
  
 本主題包含下列幾節：  
  
-   [組件物件](#Assembly)  
  
-   [Backup 與 Restore 方法](#Backup)  
  
-   [追蹤物件](#Traces)  
  
-   [CaptureLog 類別和 CaptureXML 屬性](#CaptureLog)  
  
-   [AMOException 例外狀況類別](#AMO)  
  
 下圖顯示在本主題中說明的類別關聯性。  
  
 ![AMO 其他類別](../../../analysis-services/multidimensional-models/analysis-management-objects/media/amo-otherclasses.gif "AMO 其他類別")  
  
##  <a name="Assembly"></a>組件物件  
 建立 <xref:Microsoft.AnalysisServices.Assembly> 物件的方式是將它加入伺服器的組件集合，然後使用 Update 方法將 <xref:Microsoft.AnalysisServices.Assembly> 物件更新到伺服器。  
  
 若要移除 <xref:Microsoft.AnalysisServices.Assembly> 物件，必須使用 <xref:Microsoft.AnalysisServices.Assembly> 物件的 Drop 方法來卸除它。 從資料庫的組件集合移除 <xref:Microsoft.AnalysisServices.Assembly> 物件並不會卸除組件，它只會讓您無法在應用程式中看到組件，直到下次執行應用程式為止。  
  
 如需有關可用方法和屬性的詳細資訊，請參閱<xref:Microsoft.AnalysisServices.Assembly>中<xref:Microsoft.AnalysisServices>。  
  
> [!IMPORTANT]  
>  COM 組件可能會造成安全性風險。 由於這項風險和其他考量，COM 組件在 [!INCLUDE[ssASversion10](../../../includes/ssasversion10-md.md)]中已經被取代。 在未來的版本中，可能不再支援 COM 組件。  
  
##  <a name="Backup"></a>Backup 與 Restore 方法  
 備份與還原是可用以建立 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 資料庫複本以及使用該複本復原資料庫的方法。 Backup 方法屬於 <xref:Microsoft.AnalysisServices.Database> 物件，而 Restore 方法則屬於 <xref:Microsoft.AnalysisServices.Server> 物件。  
  
 只允許伺服器和資料庫管理員執行資料庫的備份。 只有伺服器管理員可以將資料庫還原到與備份來源不同的伺服器。 資料庫管理員可以覆寫現有的資料庫以還原資料庫，只要他們擁有要覆寫的資料庫。 在還原之後，如果資料庫是用其原始安全性定義還原，資料庫管理員可能會喪失對已還原資料庫的存取權。  
  
 資料庫備份檔案必須有 .abf 副檔名。  
  
### <a name="backup-method"></a>Backup 方法  
 若要備份資料庫，請以備份檔案名稱做為參數來使用資料庫物件的 Backup 方法。  
  
##### <a name="default-values"></a>預設值：  
 AllowOverwrite=**false**  
  
 BackupRemotePartitions=**false**  
  
 Security=**CopyAll**  
  
 ApplyCompression=**true**  
  
### <a name="restore-method"></a>Restore 方法  
 若要將資料庫還原到伺服器，請以備份檔案做為參數來使用伺服器的 Restore 方法。  
  
##### <a name="default-values"></a>預設值：  
 AllowOverwrite=**false**  
  
 DataSourceType=**Remote**  
  
 Security=**CopyAll**  
  
##### <a name="restrictions"></a>限制  
  
1.  無法將本機資料分割還原為遠端資料分割。  
  
2.  無法將遠端資料分割還原為本機資料分割，但是可以將遠端資料分割還原到不同於備份來源的伺服器。  
  
### <a name="common-parameters-and-properties-for-backup-and-restore-methods"></a>Backup 與 Restore 方法的共同參數與屬性  
  
-   **檔案**的是要備份 （UNC 名稱） 的檔案名稱。  
  
-   **位置**指定伺服器特定備份的資訊，例如**BackupFile**。這可讓您指定遠端資料庫的個別備份檔案。  
  
-   **DatasourceID**指定遠端伺服器中從屬資料庫的識別碼。  
  
-   **ConnectionString**可讓您調整遠端資料來源，以防遠端伺服器已變更。 當有 ConnectionString 時，一定要指定 DatasourceID。  
  
-   **資料夾**允許重新對應至本機硬碟上的資料分割的資料夾  
  
-   **原始**為本機資料分割的原始資料夾。  
  
-   **新**是進行本機資料分割用來在相對應的 'Original' 舊資料夾中的新位置。  
  
-   **密碼**，如果不是空白，指定伺服器將加密備份檔案。  
  
##  <a name="Traces"></a>追蹤物件  
 追蹤是用於監視、重新執行和管理 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體的架構。 像 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] 等用戶端應用程式會訂閱追蹤，而且伺服器會按照追蹤定義的指定將追蹤事件傳送回去。  
  
 每個事件由事件類別描述。 事件類別描述所產生的事件類型。 在事件類別中，事件子類別描述更細的分類層級。 每個事件由若干資料行描述。 在所有事件中，描述追蹤事件的資料行都是一致的，而且符合 SQL 追蹤結構。 記錄在每一個資料行中的資訊，可能會因事件類別而不同，也就是，每個追蹤都有一組預先定義的資料行，但是資料行的意義可能會隨事件類別而不同。 例如，TextData 資料行是用以記錄所有陳述式事件的原始 ASSL。  
  
 追蹤定義可以包括同時要追蹤的一或多個事件類別。 對於每個事件類別，可以將一或多個資料行加入追蹤定義，但是不一定會使用所有的追蹤資料行。 資料庫管理員可以決定要在追蹤中包括哪些可用的資料行。 此外，可以根據追蹤中任何資料行上的篩選準則，選擇性地追蹤事件類別。  
  
 可以啟動並刪除追蹤。 可以同時執行多個追蹤。 可以即時擷取追蹤事件，或是導向檔案以供稍後分析或是重新執行之用。 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] 是用以分析和重新執行 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 追蹤事件的工具。 允許多個連接從相同的追蹤接收事件。  
  
 追蹤可以分成兩個群組：伺服器追蹤和工作階段追蹤。 伺服器追蹤將通知伺服器中的所有事件，工作階段追蹤將只會通知目前工作階段中的事件。  
  
 伺服器追蹤集合中的追蹤是以下列方式定義：  
  
1.  建立 <xref:Microsoft.AnalysisServices.Trace> 物件並擴展其基本資料，包括追蹤識別碼、名稱、記錄檔名稱、附加|覆寫等等。  
  
2.  將要監視的事件加入追蹤物件的 Events 集合。 對於每個事件，會加入資料行。  
  
3.  透過將不需要的資料列加入篩選集合，將 Filters 設定成排除它們。  
  
4.  啟動追蹤，建立追蹤並不會開始收集資料。  
  
5.  停止追蹤。  
  
6.  使用 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] 檢閱追蹤檔案。  
  
 工作階段物件中的追蹤是以下列方式取得：  
  
1.  定義函數以處理 SessionTrace 在應用程式中所產生的追蹤事件。 可能的事件是 OnEvent 及 Stopped。  
  
2.  將定義的函數加入事件處理常式。  
  
3.  啟動工作階段追蹤。  
  
4.  執行您的處理序並讓函數處理常式擷取事件。  
  
5.  停止工作階段追蹤。  
  
6.  繼續執行您的應用程式。  
  
##  <a name="CaptureLog"></a>CaptureLog 類別和 CaptureXML 屬性  
 AMO 執行的所有動作都會當做 XMLA 訊息傳送到伺服器。 AMO 提供不需 SOAP 標頭即可擷取所有這些訊息的方法。 如需詳細資訊，請參閱[簡介 AMO 類別](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)。 CaptureLog 是 AMO 中用以編寫物件與作業之指令碼的機制，將會使用 XMLA 來編寫物件與作業的指令碼。  
  
 若要開始擷取 XML，請將 CaptureXML 伺服器物件屬性必須設為**true**。 接著所有要傳送到伺服器的動作都會在 CaptureLog 類別中開始擷取，而不必將動作傳送到伺服器。 CaptureLog 被視為類別，因為它有 Clear 這個可用來清除擷取記錄的方法。  
  
 若要讀取記錄，請取得字串集合並開始對字串反覆運算。 另外，您可以使用伺服器物件方法 ConcatenateCaptureLog，將所有的記錄串連成一個字串。 ConcatenateCaptureLog 有三個參數，其中有兩個是必要的。 必要的參數*異動*，是布林類型，和*平行*，是布林類型。 如果*異動*設**true**，它會指出因為在單一交易，而不是每個命令視為個別交易，將建立的 XML 批次檔。 如果*平行*設**true**，它會指出以並行執行，而不是依序將記錄的批次檔中的所有命令，為都記錄。  
  
##  <a name="AMO"></a>AMOException 例外狀況類別  
 您可以使用 AMOException 例外狀況類別，輕鬆地擷取應用程式中由 AMO 擲回的例外狀況。  
  
 AMO 在找到不同的問題時將會擲回例外狀況。 下表列出 AMO 所處理的例外狀況種類。 例外狀況是從 <xref:Microsoft.AnalysisServices.AmoException> 類別衍生。  
  
|例外狀況|起源|Description|  
|---------------|------------|-----------------|  
|<xref:Microsoft.AnalysisServices.AmoException>|基底類別|當必要的父物件遺失時，或是當集合中找不到要求的項目時，應用程式會收到這個例外狀況。|  
|<xref:Microsoft.AnalysisServices.OutOfSyncException>|衍生自 AMOException|當 AMO 與引擎不同步，而且引擎傳回 AMO 不認識的物件參考時，應用程式會收到這個例外狀況。|  
|<xref:Microsoft.AnalysisServices.OperationException>|衍生自 AMOException|這是應用程式經常收到的重要例外狀況。 這個例外狀況包含來自伺服器的錯誤詳細資料，有可能是因為 Update、Process 或 Drop 等錯誤的 AMO 作業所造成。|  
|<xref:Microsoft.AnalysisServices.ResponseFormatException>|衍生自 AMOException|當引擎以 AMO 不了解的格式傳回訊息時，就會發生這個例外狀況。|  
|<xref:Microsoft.AnalysisServices.ConnectionException>|衍生自 AMOException|當無法 (以 Server.Connect ) 建立連接，或是當 AMO 與引擎通訊而遺失連接時 (例如在 Update、Process 或 Drop 期間)，就會發生這個例外狀況。|  
  
## <a name="see-also"></a>另請參閱  
 <xref:Microsoft.AnalysisServices>   
 [AMO 類別簡介](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [邏輯架構 & #40;Analysis Services-多維度資料 & #41;](../../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [資料庫物件 & #40;Analysis Services-多維度資料 & #41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  
