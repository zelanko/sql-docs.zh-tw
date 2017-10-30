---
title: "Integration Services (SSIS) 記錄 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.configuredtslogs.containers.f1
- sql13.dts.designer.configuredtslogs.loggingdetails.f1
- sql13.dts.designer.configuredtslogs.providersandlogs.f1
- SQL13.SSIS.SSMS.ISMANAGECUSTOMIZEDLOGGINGLEVEL.F1
helpviewer_keywords:
- containers [Integration Services], logs
- Windows Event log provider [Integration Services]
- XML File log provider [Integration Services]
- SQL Server Profiler, log provider
- SQL Server Integration Services packages, logs
- SSIS packages, logs
- tasks [Integration Services], logs
- logs [Integration Services], log providers
- Integration Services packages, logs
- log providers [Integration Services]
- packages [Integration Services], logs
- Text File log provider
- SQL Server log provider
ms.assetid: 65e17889-371f-4951-9a7e-9932b2d0dcde
caps.latest.revision: 69
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: c3e47e4a5ae297202ba43679fba393421880a7ea
ms.openlocfilehash: 22c1126b8d5555dc743f7c8906230cf5dbcb08a8
ms.contentlocale: zh-tw
ms.lasthandoff: 09/28/2017

---
# <a name="integration-services-ssis-logging"></a>Integration Services (SSIS) 記錄
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包括可用於在封裝、容器和工作中實作記錄的記錄提供者。 使用記錄，可以擷取有關封裝的執行階段資訊，藉此幫助您在每次執行封裝時對其進行稽核和疑難排解。 例如，記錄可以擷取執行封裝之操作員的名稱，以及封裝開始和結束的時間。  
  
 您可以設定在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器上的封裝執行期間發生的記錄範圍。 如需詳細資訊，請參閱 [在 SSIS 伺服器上啟用封裝執行的記錄功能](#server_logging)。  
  
 您還可以在使用 **dtexec** 命令提示公用程式執行封裝時，併入記錄功能。 如需支援記錄功能之命令提示引數的詳細資訊，請參閱 [dtexec 公用程式](../../integration-services/packages/dtexec-utility.md)。  
  
## <a name="configure-logging-in-sql-server-data-tools"></a>設定 SQL Server Data Tools 中的記錄功能  
 記錄與封裝相關聯，並在封裝層級設定。 封裝中的每個工作或容器都可將資訊記錄至任何封裝記錄檔中。 您可以啟用封裝中工作和容器的記錄功能，即使該封裝本身未啟用記錄功能。 例如，可以在「執行 SQL」工作上啟用記錄功能，而無需在父封裝上啟用記錄功能。 封裝、容器或工作可以寫入多重記錄檔。 您可以僅在封裝上啟用記錄功能，也可以選擇在封裝所包含的任何個別工作或容器上啟用記錄功能。  
  
 當您將記錄加入封裝時，請選擇記錄提供者和記錄的位置。 記錄提供者會指定記錄資料的格式：例如， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫或文字檔。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包括下列記錄提供者：  
  
-   「文字檔」記錄提供者，它會將記錄項目以逗號分隔值 (CSV) 的格式寫入 ASCII 文字檔。 此提供者的預設副檔名為 .log。  
  
-   [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 記錄提供者，它可寫入追蹤檔，您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler 檢視該追蹤檔。 此提供者的預設副檔名為 .trc。  
  
    > [!NOTE]  
    >  您無法在以 64 位元模式執行的封裝中使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 記錄提供者。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記錄提供者，它可將記錄項目寫入 **資料庫的** sysssislog [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表中。  
  
-   「Windows 事件」記錄提供者，它可將項目寫入本機電腦上之「Windows 事件」記錄的「應用程式」記錄中。  
  
-   「XML 檔案」記錄提供者，它可將記錄檔寫入 XML 檔案中。 此提供者的預設副檔名為 .xml。  
  
 如果您將記錄提供者加入封裝或以程式設計的方式設定記錄，則可以使用 ProgID 或 ClassID 來識別記錄提供者，以取代使用 [設定 SSIS 記錄] 對話方塊中所顯示之 [[!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師] 的名稱。  
  
 下表列出 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 所包含之記錄提供者的 ProgID 和 ClassID，以及記錄提供者寫入記錄檔的位置。  
  
|記錄提供者|ProgID|ClassID|位置|  
|------------------|------------|-------------|--------------|  
|文字檔|DTS.LogProviderTextFile|{0A039101-ACC1-4E06-943F-279948323883}|記錄提供者所使用的「檔案」連接管理員會指定文字檔的路徑。|  
|SQL Server Profiler|DTS.LogProviderSQLProfiler|{E93F6300-AE0C-4916-A7BF-A8D0CE12C77A}|記錄提供者所使用的「檔案」連線管理員會指定 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]所使用之檔案的路徑。|  
|SQL Server|DTS.LogProviderSQLServer|{94150B25-6AEB-4C0D-996D-D37D1C4FDEDA}|記錄提供者所使用的 OLE DB 連線管理員會指定包含具有記錄項目之 sysssislog 資料表的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。|  
|Windows 事件記錄檔|DTS.LogProviderEventLog|{071CC8EB-C343-4CFF-8D58-564B92FCA3CF}|Windows 事件檢視器中的應用程式記錄檔包含 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 記錄資訊。|  
|XML 檔案|DTS.LogProviderXMLFile|{440945A4-2A22-4F19-B577-EAF5FDDC5F7A}|記錄提供者所使用的「檔案」連接管理員會指定 XML 檔案的路徑。|  
  
 您還可以建立自訂記錄提供者。 如需詳細資訊，請參閱 [建立自訂記錄提供者](../../integration-services/extending-packages-custom-objects/log-provider/creating-a-custom-log-provider.md)。  
  
 封裝中的記錄提供者是此封裝之記錄提供者集合的成員。 使用 [[!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師] 建立封裝並實作記錄時，您可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師的 [封裝總管] 索引標籤上，看到 [記錄提供者] 資料夾中集合成員的清單。  
  
 您可以藉由提供記錄提供者的名稱和描述，並指定記錄提供者使用的連接管理員，來設定記錄提供者。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記錄提供者會使用 OLE DB 連接管理員。 「文字檔」、「 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]」和「XML 檔案」記錄提供者全都使用「檔案」連線管理員。 Windows 事件記錄檔提供者不使用連接管理員，因為它會直接寫入「Windows 事件記錄檔」中。 如需詳細資訊，請參閱 [OLE DB 連線管理員](../../integration-services/connection-manager/ole-db-connection-manager.md) 和 [檔案連線管理員](../../integration-services/connection-manager/file-connection-manager.md)。  
  
### <a name="logging-customization"></a>自訂記錄  
 為了自訂事件或自訂訊息的記錄， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供通常記錄之資訊的結構描述，以用於併入記錄項目。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 記錄結構描述會定義可以記錄的資訊。 您可以從記錄結構描述選擇每個記錄項目的元素。  
  
 封裝及其容器和工作不一定要記錄相同資訊，相同封裝或容器內的工作也可以記錄不同的資訊。 例如，封裝可以在封裝啟動時記錄操作員資訊，一個工作可以記錄工作失敗的來源，而另一個工作可以在發生錯誤時記錄資訊。 如果封裝及其容器和工作使用多重記錄檔，則相同的資訊會寫入所有記錄檔中。  
  
 您可以指定要記錄的事件和每個事件要記錄的資訊，以選取符合您需要的記錄層級。 您可能會發現某些事件提供的資訊比其他事件更有用。 例如，您可能只想記錄 **PreExecute** 事件的電腦和操作員名稱，而不是 **Error** 事件的所有可用資訊。  
  
 若要防止記錄檔使用大量的磁碟空間，或避免可能會降低效能的過度記錄，可以選取要記錄的特定事件和資訊項目，以限制記錄。 例如，您可以設定記錄檔僅擷取每個錯誤的日期和電腦名稱。  
  
 在 [[!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師] 中，使用 [設定 SSIS 記錄] 對話方塊來定義記錄選項。  
  
#### <a name="log-schema"></a>記錄結構描述  
 下表描述記錄結構描述中的元素。  
  
|元素|說明|  
|-------------|-----------------|  
|電腦|發生記錄事件之電腦的名稱。|  
|運算子|啟動封裝之使用者的識別。|  
|SourceName|發生記錄事件之容器或工作的名稱。|  
|SourceID|封裝的唯一識別碼；「For 迴圈」、「Foreach 迴圈」或「時序」容器；或者發生記錄事件的工作。|  
|ExecutionID|封裝執行執行個體的 GUID。<br /><br /> 請注意：執行單一封裝可能會建立記錄項目，其中包含不同的 ExecutionID 元素值。 例如，當您在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中執行封裝時，驗證階段可能會建立記錄項目，其中包含了對應到 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]的 ExecutionID 元素。 但是，執行階段可能會建立記錄項目，其中包含了對應到 dtshost.exe 的 ExecutionID 元素。 在另一個範例中，當您執行包含「執行封裝」工作的封裝時，每一個工作都會執行子封裝。 這些子封裝可能會建立記錄項目，其中包含了與父封裝建立之記錄項目不同的 ExecutionID 元素。|  
|MessageText|與記錄項目相關聯的訊息。|  
|DataBytes|記錄項目特定的位元組陣列。 此欄位的意義會因記錄項目的不同而不同。|  
  
 下表描述記錄結構描述中，在 [設定 SSIS 記錄] 對話方塊的 [詳細資料] 索引標籤上沒有提供的三個額外元素。  
  
|元素|說明|  
|-------------|-----------------|  
|StartTime|容器或工作開始執行的時間。|  
|EndTime|容器或工作停止執行的時間。|  
|DataCode|選擇性的整數值，一般會包含 <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult> 列舉的值，指出執行容器或工作的結果：<br /><br /> 0 - 成功<br /><br /> 1 - 失敗<br /><br /> 2 - 已完成<br /><br /> 3 - 已取消|  
  
#### <a name="log-entries"></a>記錄項目  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 支援預先定義事件上的記錄項目，並為許多 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 物件提供自訂記錄項目。 在 [[!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師] 中的 [設定 SSIS 記錄] 對話方塊會列出這些事件和自訂記錄項目。  
  
 下表描述的預先定義事件可在發生執行階段事件時寫入記錄項目。 這些記錄項目會套用至可執行檔、封裝和封裝所包含的工作和容器。 記錄項目的名稱與引發並造成寫入記錄項目之執行階段事件的名稱相同。  
  
|事件|說明|  
|------------|-----------------|  
|**OnError**|發生錯誤時寫入記錄項目。|  
|**OnExecStatusChanged**|當工作 (非容器) 在偵錯期間暫停或繼續時，寫入記錄項目。|  
|**OnInformation**|在驗證和執行可執行檔以報告資訊期間，寫入記錄項目。|  
|**OnPostExecute**|在可執行檔已完成執行後立即寫入記錄項目。|  
|**OnPostValidate**|在完成驗證可執行檔時寫入記錄項目。|  
|**OnPreExecute**|在可執行檔執行前立即寫入記錄項目。|  
|**OnPreValidate**|在啟動驗證可執行檔時寫入記錄項目。|  
|**OnProgress**|在可執行檔處理可量值進度時寫入記錄項目。|  
|**OnQueryCancel**|在工作處理期間任何可取消執行的時間點寫入記錄項目。|  
|**OnTaskFailed**|在工作失敗時寫入記錄項目。|  
|**OnVariableValueChanged**|在變數的值變更時寫入記錄項目。|  
|**OnWarning**|發生警告時寫入記錄項目。|  
|**PipelineComponentTime**|針對每個資料流程元件，寫入每個驗證和執行階段的記錄項目。 記錄項目會指定每個階段的處理時間。|  
|**Diagnostic**<br /><br /> **DiagnosticEx**|寫入提供診斷資訊的記錄項目。<br /><br /> 例如，您可以在每次呼叫外部資料提供者前後記錄訊息。 如需詳細資訊，請參閱 [封裝執行的疑難排解工具](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)。<br /><br /> 當您想要在有錯誤的資料流程資料行中尋找資料行名稱時，請記錄 **DiagnosticEx** 事件。 此事件會將資料流程歷程對應寫入記錄檔。 您接著可以使用錯誤輸出所擷取的資料行識別碼，在此歷程對應中查詢資料行名稱。 如需詳細資訊，請參閱＜ [Error Handling in Data](../../integration-services/data-flow/error-handling-in-data.md)＞。<br /><br /> 請注意， **DiagnosticEx** 事件不會在其 XML 輸出中保留空白，以縮減記錄檔的大小。 若要改善可讀性，可將記錄檔複製到 XML 編輯器 (例如，在 Visual Studio 中)，該編輯器需支援 XML 格式設定和語法反白顯示。<br /><br /> 注意︰如果使用 SQL Server 記錄提供者來記錄 **DiagnosticEx** 事件，輸出可能被截斷。 SQL Server 記錄提供者的 [訊息] 欄位類型是 nvarchar(2048)。 若要避免發生截斷，記錄 **DiagnosticEx** 事件時請使用不同的記錄提供者。|  
  
 封裝及許多工作都有可以啟用記錄功能的自訂記錄項目。 例如，[傳送郵件] 工作會提供 **SendMailTaskBegin** 自訂記錄項目，其會在 [傳送郵件] 工作開始執行時，但在工作傳送電子郵件訊息之前，記錄資訊。 如需詳細資訊，請參閱 [自訂訊息以進行記錄](#custom_messages)。  
  
### <a name="differentiating-package-copies"></a>區分封裝副本  
 記錄資料包含記錄項目所屬封裝的名稱和 GUID。 如果您透過複製現有的封裝來建立新的封裝，將一併複製現有封裝的名稱和 GUID。 因此，您可能會有兩套具有相同 GUID 和名稱的封裝，使您難以區分記錄資料中的封裝。  
  
 為了消除這種模糊不清的狀況，您應該更新這個新封裝的名稱和 GUID。 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，您可以在 [屬性] 視窗的 **ID** 屬性中重新產生 GUID，並更新 **Name** 屬性的值。 您也可以使用程式設計方式或 **dtutil** 命令提示字元來變更 GUID 和名稱。 如需詳細資訊，請參閱 [設定封裝屬性](../../integration-services/set-package-properties.md) 和 [dtutil 公用程式](../../integration-services/dtutil-utility.md)。  
  
### <a name="parent-logging-options"></a>父記錄選項  
 通常，工作和「For 迴圈」、「Foreach 迴圈」和「時序」容器的記錄選項符合封裝或父容器的選項。 在該情況下，可以設定它們從其父容器繼承記錄選項。 例如，在包含「執行 SQL」工作的「For 迴圈」容器中，「執行 SQL」工作可以使用在「For 迴圈」容器上設定的記錄選項。 若要使用父記錄選項，可將容器的 LoggingMode 屬性設為 **UseParentSetting**。 可以在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 的 [屬性] 視窗中，或透過 [[!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師] 的 [設定 SSIS 記錄] 對話方塊設定此屬性。  
  
### <a name="logging-templates"></a>記錄範本  
 在 [設定 SSIS 記錄] 對話方塊中，還可以將常用的記錄組態建立和儲存為範本，然後在多個封裝中使用這些範本。 這使得跨多個封裝套用一致的記錄策略，以及修改封裝的記錄設定變得很容易，只要更新後再套用範本即可。 範本以 XML 檔案儲存。  
  
 **若要使用 [設定 SSIS 記錄] 對話方塊設定記錄**  
  
1.  啟用封裝及其工作的記錄功能。 記錄可以發生在封裝、容器和工作層級上。 您可以為封裝、容器和工作指定不同的記錄檔。  
  
2.  選取記錄提供者，並為封裝加入記錄。 記錄檔僅可以在封裝層級建立，且工作或容器必須使用為封裝建立的記錄檔之一。 每個記錄檔都與下列記錄提供者之一相關聯：文字檔、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、Windows 記錄檔或 XML 檔案。 如需詳細資訊，請參閱 [在 SQL Server Data Tools 中啟用封裝記錄功能](#ssdt)。  
  
3.  選取事件，以及要在記錄檔中擷取之每個事件的記錄結構描述資訊。 如需詳細資訊，請參閱 [使用已儲存的組態檔來設定記錄](#saved_config)。  
  
### <a name="configuration-of-log-provider"></a>設定記錄提供者  
 您可以透過「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」或以程式設計方式設定屬性。  
  
 記錄提供者是按照在封裝中實作記錄的步驟而建立和設定的。  
  
 建立記錄提供者之後，您可以在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]的 [屬性] 視窗中檢視和修改其屬性。  
  
 如需以程式設計方式設定這些屬性的詳細資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider> 類別的文件。  
  
### <a name="logging-for-data-flow-tasks"></a>資料流程工作的記錄功能  
 資料流程工作提供許多可用以監視及調整效能的自訂記錄項目。 例如，您可以監視可能會造成記憶體遺漏的元件，或是追蹤執行某特定元件所花費的時間。 如需這些自訂記錄項目的清單以及記錄輸出範例，請參閱 [資料流程工作](../../integration-services/control-flow/data-flow-task.md)。  
  
#### <a name="capture-the-names-of-columns-in-which-errors-occur"></a>擷取發生錯誤的資料行名稱  
 當您設定資料流的錯誤輸出時，錯誤輸出預設只提供發生錯誤的資料行數值識別碼。 如需詳細資訊，請參閱＜ [Error Handling in Data](../../integration-services/data-flow/error-handling-in-data.md)＞。  
  
 您可以啟用記錄並選取 **DiagnosticEx** 事件，找到資料行名稱。 此事件會將資料流程歷程對應寫入記錄檔。 接著從這個歷程對應中的資料行識別項，查閱資料行名稱。 請注意， **DiagnosticEx** 事件不會在其 XML 輸出中保留空白，以縮減記錄檔的大小。 若要改善可讀性，可將記錄檔複製到 XML 編輯器 (例如，在 Visual Studio 中)，該編輯器需支援 XML 格式設定和語法反白顯示。  
  
#### <a name="use-the-pipelinecomponenttime-event"></a>使用 PipelineComponentTime 事件  
 最有用的自訂記錄項目可能是 PipelineComponentTime 事件。 這個記錄項目會報告每個元件在五個主要處理步驟的每個步驟中所花費的毫秒數。 下表描述這些處理步驟。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 開發人員會將這些步驟辨識為 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>。  
  
|步驟|說明|  
|----------|-----------------|  
|Validate|元件會檢查有效的屬性值和組態設定。|  
|PreExecute|元件會在開始處理資料列之前，執行一次處理。|  
|PostExecute|元件會在已經處理所有資料列之後，執行一次處理。|  
|ProcessInput|轉換或目的地元件會處理上游來源或轉換傳遞給它的傳入資料列。|  
|PrimeOutput|來源或轉換元件會填入要傳遞給下游轉換或目的地元件的資料緩衝區。|  
  
 當您啟用 PipelineComponentTime 事件時， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 就會針對每個元件所執行的每個處理步驟記錄一則訊息。 下列記錄項目會顯示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] CalculatedColumns 封裝範例所記錄的訊息子集：  
  
 `The component "Calculate LineItemTotalCost" (3522) spent 356 milliseconds in ProcessInput.`  
  
 `The component "Sum Quantity and LineItemTotalCost" (3619) spent 79 milliseconds in ProcessInput.`  
  
 `The component "Calculate Average Cost" (3662) spent 16 milliseconds in ProcessInput.`  
  
 `The component "Sort by ProductID" (3717) spent 125 milliseconds in ProcessInput.`  
  
 `The component "Load Data" (3773) spent 0 milliseconds in ProcessInput.`  
  
 `The component "Extract Data" (3869) spent 688 milliseconds in PrimeOutput filling buffers on output "OLE DB Source Output" (3879).`  
  
 `The component "Sum Quantity and LineItemTotalCost" (3619) spent 141 milliseconds in PrimeOutput filling buffers on output "Aggregate Output 1" (3621).`  
  
 `The component "Sort by ProductID" (3717) spent 16 milliseconds in PrimeOutput filling buffers on output "Sort Output" (3719).`  
  
 這些記錄項目顯示資料流程工作將大部分時間花費在下列步驟上 (在此依遞減順序顯示)：  
  
-   名為 "Extract Data" 的 OLE DB 來源花費了 688 毫秒 來載入資料。  
  
-   名為 "Calculate LineItemTotalCost" 的「衍生的資料行」轉換花費了 356 毫秒 來計算傳入資料列。  
  
-   名為 "Sum Quantity and LineItemTotalCost" 的「彙總」轉換花費了結合的 220 毫秒 (141 毫秒在 PrimeOutput 而 79 毫秒在 ProcessInput) 來執行計算以及將資料傳遞給下一個轉換。  

## <a name="ssdt"></a> 在 SQL Server Data Tools 中啟用封裝記錄功能
  本程序描述如何將記錄檔加入封裝、設定封裝層級的記錄，以及將記錄組態儲存至 XML 檔案。 您可以僅在封裝層級加入記錄檔，但封裝無需執行記錄即可啟用封裝所包含之容器中的記錄。  
  
> [!IMPORTANT]  
>  如果您將 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器，則您為封裝執行設定的記錄層次會覆寫您使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]設定的封裝記錄。  
  
 依預設，封裝中的容器使用與其父容器相同的記錄組態。 如需設定個別容器之記錄選項的資訊，請參閱 [使用已儲存的組態檔來設定記錄](#saved_config)。  
  
### <a name="to-enable-logging-in-a-package"></a>若要啟用封裝中的記錄  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 **[SSIS]** 功能表上，按一下 **[記錄]**。  
  
3.  在 提供者類型 清單中選取記錄提供者，然後按一下加入。  
  
4.  在**組態**資料行中，選取連接管理員，或按一下**\<新增連接 >**為記錄提供者建立新的連接管理員適當的型別。 因所選提供者的不同，使用下列連接管理員之一：  
  
    -   若為「文字」檔案，請使用「檔案」連接管理員。 如需詳細資訊，請參閱 [檔案連線管理員](../../integration-services/connection-manager/file-connection-manager.md)  
  
    -   若為 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]，請使用檔案連線管理員。  
  
    -   若為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，請使用 OLE DB 連接管理員。 如需相關資訊，請參閱 [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md)。  
  
    -   若為 Windows 事件記錄檔，不需任何動作。 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 會自動建立記錄檔。  
  
    -   若為 XML 檔案，請使用「檔案」連接管理員。  
  
5.  針對封裝中要使用的每個記錄檔重複步驟 3 和 4。  
  
    > [!NOTE]  
    >  封裝可以使用每種類型一個以上的記錄檔。  
  
6.  選擇性地選取封裝層級核取方塊，並選取要用於封裝層級記錄的記錄檔，然後按一下詳細資料 索引標籤。  
  
7.  在 [詳細資料] 索引標籤上，選取 [事件]，以記錄所有記錄項目，或清除 [事件]，以選取個別事件。  
  
8.  選擇性地按一下 [進階]，以指定要記錄哪些資訊。  
  
    > [!NOTE]  
    >  依預設，會記錄所有資訊。  
  
9. 在 [詳細資料] 索引標籤上，按一下 [儲存]。 [另存新檔] 對話方塊隨即出現。 尋找要儲存記錄組態的資料夾，輸入新記錄組態的檔案名稱，然後按一下儲存。  
  
10. 按一下 **[確定]**。  
  
11. 若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  

## <a name="configure_logs"></a> 設定 SSIS 記錄對話方塊
  使用 **[設定 SSIS 記錄]** 對話方塊定義封裝的記錄選項。  
  
 **您想要做什麼事？**  
  
1.  [開啟 [設定 SSIS 記錄] 對話方塊。](#open_dialog)  
  
2.  [設定 [容器] 窗格中的選項](#container)  
  
3.  [設定 [提供者與記錄] 索引標籤上的選項](#provider)  
  
4.  [設定 [詳細資料] 索引標籤上的選項](#detail)  
  
###  <a name="open_dialog"></a> 開啟 [設定 SSIS 記錄] 對話方塊。  
 **開啟 [設定 SSIS 記錄] 對話方塊**  
  
-   在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中，按一下 **[SSIS]** 功能表上的 **[記錄]** 。  
  
###  <a name="container"></a> 設定 [容器] 窗格中的選項  
 使用 **[設定 SSIS 記錄]** 對話方塊的 **[容器]** 窗格，即可啟用封裝及其容器以進行記錄。  
  
#### <a name="options"></a>選項。  
 **[設定 SSIS 記錄]**  
 在階層式檢視中選取核取方塊，即可啟用封裝及其容器以進行記錄：  
  
-   如果已清除，則表示並未啟用容器來進行記錄。 選取即可啟用記錄。  
  
-   如果呈暗灰色，容器就會使用其父系的記錄選項。 封裝無法使用此選項。  
  
-   如果已核取，則容器會定義它自己的記錄選項。  
  
 如果容器呈暗灰色，而您要在容器上設定記錄選項，請按兩下其核取方塊。 第一次點選時會清除核取方塊，而第二次點選則會選取核取方塊，讓您可以選擇要使用的記錄提供者和選取要記錄的資訊。  
  
###  <a name="provider"></a> 設定 [提供者與記錄] 索引標籤上的選項  
 使用 [設定 SSIS 記錄] 對話方塊的 [提供者與記錄] 索引標籤，即可建立和設定用於擷取執行階段事件的記錄。  
  
#### <a name="options"></a>選項。  
 **提供者類型**  
 從清單中選取記錄提供者的類型。  
  
 **加入**  
 將所指定類型的記錄加入至封裝之記錄提供者的集合。  
  
 **名稱**  
 使用這些核取方塊，啟用或停用容器的記錄，或是 [設定 SSIS 記錄] 對話方塊的 [容器] 窗格中選取之工作的記錄。 名稱欄位是可編輯的。 使用提供者的預設名稱，或輸入唯一的描述性名稱。  
  
 **說明**  
 描述欄位是可編輯的。 按一下，然後修改記錄的預設描述。  
  
 **Configuration**  
 在清單中，選取現有的連接管理員，或按一下\<**新增連接...**> 以建立新的連接管理員。 視記錄提供者的類型而定，您可以設定 OLE DB 連接管理員或檔案連接管理員。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 事件記錄檔的記錄提供者不需要有連接。  
  
 相關主題： [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md) 、 [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)  
  
 **Delete**  
 選取記錄提供者，然後按一下刪除。  
  
###  <a name="detail"></a> 設定 [詳細資料] 索引標籤上的選項  
 使用 **[設定 SSIS 記錄]** 對話方塊的 **[詳細資料]** 索引標籤，即可指定要啟用記錄的事件以及要記錄的資訊詳細資料。 您選取的資訊適用於封裝中的所有記錄提供者。 例如，您無法寫入部份資訊到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，而寫入不同資訊到文字檔。  
  
#### <a name="options"></a>選項。  
 **事件**  
 啟用或停用記錄事件。  
  
 **說明**  
 檢視事件的描述。  
  
 **進階**  
 選取或清除要記錄的事件，以及選取或清除要為每個事件記錄的資訊。 按一下 **[基本]** ，即可隱藏除了事件清單以外的所有記錄詳細資料。 記錄可以使用下列資訊：  
  
|Value|說明|  
|-----------|-----------------|  
|**電腦**|記錄事件發生所在之電腦的名稱。|  
|**運算子**|啟動封裝之人員的使用者名稱。|  
|**SourceName**|記錄事件發生所在之封裝、容器或工作的名稱。|  
|**SourceID**|記錄事件發生所在之封裝、容器或工作的全域唯一識別碼 (GUID)。|  
|**ExecutionID**|封裝執行個體的全域唯一識別碼。|  
|**MessageText**|與記錄項目相關聯的訊息。|  
|**DataBytes**|保留供日後使用。|  
  
 **[基本]**  
 選取或清除要記錄的事件。 此選項會隱藏除了事件清單以外的記錄詳細資料。 依預設，如果您選取某個事件，該事件的所有記錄詳細資料都會被選取。 按一下 **[進階]** ，即可顯示所有的記錄詳細資料。  
  
 **載入**  
 指定現有的 XML 檔案，即可用來作為設定記錄選項的範本。  
  
 **儲存**  
 將組態詳細資料儲存為 XML 檔案的範本。  

## <a name="saved_config"></a> 使用已儲存的組態檔來設定記錄
  此程序描述如何透過載入先前儲存的記錄組態檔，為封裝中的新容器設定記錄。  
  
 依預設，封裝中的所有容器都使用與其父容器相同的記錄組態。 例如，「Foreach 迴圈」中的工作會使用與「Foreach 迴圈」相同的記錄組態。  
  
### <a name="to-configure-logging-for-a-container"></a>若要設定容器的記錄  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 **[SSIS]** 功能表上，按一下 **[記錄]**。  
  
3.  展開封裝樹狀檢視，並選取要設定的容器。  
  
4.  在 [提供者與記錄] 索引標籤上，選取要用於容器的記錄檔。  
  
    > [!NOTE]  
    >  您只可在封裝層級建立記錄檔。 如需詳細資訊，請參閱[在 SQL Server Data Tools 中啟用封裝記錄功能](#ssdt)。  
  
5.  按一下 [詳細資料] 索引標籤，然後按一下 [載入]。  
  
6.  尋找要使用的記錄組態檔，然後按一下 [開啟]。  
  
7.  (選擇性) 在 [事件] 資料行中選取核取方塊，以選取要記錄的另一個記錄項目。 按一下 [進階]，選取此項目所要記錄的資訊類型。  
  
    > [!NOTE]  
    >  新容器可能會包含原來用於建立記錄組態之容器無法使用的其他記錄項目。 如果您要記錄這些其他記錄項目，則必須手動選取之。  
  
8.  若要儲存記錄組態的更新版本，請按一下 [儲存]。  
  
9. 若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  

## <a name="server_logging"></a> 在 SSIS 伺服器上啟用封裝執行的記錄功能
  本主題描述如何在執行已部署至 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器的封裝時，設定或變更封裝的記錄層級。 執行封裝時設定的記錄層級會覆寫您在設計期間於 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中設定的封裝記錄。 如需詳細資訊，請參閱[在 SQL Server Data Tools 中啟用封裝記錄功能](#ssdt)。  
  
 在 SQL Server 的 [伺服器屬性] 中，您可以在 [伺服器記錄層級] 屬性下方，選取預設的全伺服器記錄層級。 您可以挑選本主題所說明的其中一個內建記錄層級，或者可挑選現有的自訂記錄層級。 選取的記錄層級預設會套用到所有部署到 SSIS 目錄的封裝。 它預設也會套用到執行 SSIS 封裝的 SQL 代理程式工作步驟。  
  
 您可以使用下列其中一個方法來指定個別封裝的記錄層級。 本主題涵蓋第一個方法。  
  
-   使用執行封裝對話方塊設定封裝執行作業的執行個體  
  
-   請使用 [catalog.set_execution_parameter_value &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md) 為執行的執行個體設定參數。  
  
-   使用 [新增作業步驟] 對話方塊設定封裝執行作業的 SQL Server Agent 作業。  
  
### <a name="set-the-logging-level-for-a-package-by-using-the-execute-package-dialog-box"></a>使用執行封裝對話方塊設定封裝的記錄層級  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的 [物件總管] 中，導覽至封裝。  
  
2.  以滑鼠右鍵按一下封裝，然後選取 [執行]。  
  
3.  在 **[執行封裝]** 對話方塊中，選取 **[進階]** 索引標籤。  
  
4.  在 **[記錄層次]**底下，選取記錄層次。 本主題包含可用值的描述。  
  
5.  完成任何其他封裝組態，然後按一下 **[確定]** 執行封裝。  
  
### <a name="select-a-logging-level"></a>選取記錄層級  
 下面是可用的內建記錄層級。 您也可以選取現有的自訂記錄層級。 本主題包含自訂記錄層級的描述。  
  
|[記錄層次]|說明|  
|-------------------|-----------------|  
|無|關閉記錄功能。 只記錄封裝執行狀態。|  
|Basic|記錄所有事件，自訂和診斷事件除外。 這是預設值。|  
|RuntimeLineage|收集追蹤資料流程中歷程資訊所需的資料。 您可以剖析此歷程資訊，以對應工作間的歷程關聯性。 ISV 和開發人員可以使用此資訊來建置自訂歷程對應工具。|  
|效能|只記錄效能統計資料，以及 OnError 和 OnWarning 事件。<br /><br /> **[執行效能]** 報表會顯示封裝資料流程元件的 [啟用時間] 和 [總時間]。 最後一個封裝執行作業的記錄層次設定為 **[效能]** 或 **[詳細資訊]**時，就可使用這項資訊。 如需詳細資訊，請參閱 [Reports for the Integration Services Server](../../integration-services/performance/monitor-running-packages-and-other-operations.md#reports)。<br /><br /> [catalog.execution_component_phases](../../integration-services/system-views/catalog-execution-component-phases.md) 檢視會顯示每一個執行階段之資料流程元件的開始和結束時間。 此檢視只會在封裝執行作業的記錄層次設定為 **[效能]** 或 **[詳細資訊]**時，顯示這些元件的這項資訊。|  
|[詳細資訊]|記錄所有事件，包括自訂和診斷事件。<br /><br /> 自訂事件包括 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 工作所記錄的事件。 如需有關自訂事件的詳細資訊，請參閱 [Custom Messages for Logging](#custom_messages)。<br /><br /> **DiagnosticEx** 事件即為診斷事件的範例。 每當「執行封裝」工作執行子封裝時，此事件就會擷取傳遞至子封裝的參數值。<br /><br /> **DiagnosticEx** 事件也可協助您取得發生資料列層級錯誤的資料行名稱。 此事件會將資料流程歷程對應寫入記錄檔。 您接著可以使用錯誤輸出所擷取的資料行識別碼，在此歷程對應中查詢資料行名稱。  如需詳細資訊，請參閱＜ [Error Handling in Data](../../integration-services/data-flow/error-handling-in-data.md)＞。<br /><br /> **DiagnosticEx** 的訊息資料行值是 XML 文字。 若要檢視封裝執行的訊息文字，請查詢 [catalog.operation_messages &#40;SSISDB 資料庫&#41;](../../integration-services/system-views/catalog-operation-messages-ssisdb-database.md) 檢視。 請注意， **DiagnosticEx** 事件不會在其 XML 輸出中保留空白，以縮減記錄檔的大小。 若要改善可讀性，可將記錄檔複製到 XML 編輯器 (例如，在 Visual Studio 中)，該編輯器需支援 XML 格式設定和語法反白顯示。<br /><br /> 每當資料流程元件傳送資料至封裝執行的下游元件， [catalog.execution_data_statistics](../../integration-services/system-views/catalog-execution-data-statistics.md) 檢視就會顯示一個資料列。 您必須將記錄層次設定為 **[詳細資訊]** ，以擷取檢視中的這項資訊。|  
  
### <a name="create-and-manage-customized-logging-levels-by-using-the-customized-logging-level-management-dialog-box"></a>使用自訂的記錄層級管理對話方塊建立和管理自訂的記錄層級  
 您可以建立自訂的記錄層級，只收集您所需的統計資料和事件。 您也可以選擇性擷取事件的內容，包括變數值、連接字串及元件屬性。 當您執行封裝時，每當您可以選取內建記錄層級時，就能選取自訂的記錄層級。  
  
> [!TIP]  
>  若要擷取封裝變數的值，變數的 **IncludeInDebugDump** 屬性必須設定為 [True]。  
  
1.  若要建立和管理自訂的記錄層級，在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，以滑鼠右鍵按一下 SSISDB 資料庫，然後選取 [自訂的記錄層級] 以開啟 [自訂記錄層級管理] 對話方塊。 [自訂的記錄層級]  清單包含所有現有的自訂記錄層級。  
  
2.  若要 **建立** 新的自訂記錄層級，可按一下 [建立] ，然後提供名稱和描述。 在 [統計資料]  和 [事件]  索引標籤上，選擇您想要收集的統計資料與事件。 在 [事件]  索引標籤上，選擇性地選取個別事件的 [包含內容]  。 然後按一下 [儲存] 。  
  
3.  若要 **更新** 現有的自訂記錄層級，可在清單中選取該層級、重新進行設定，然後按一下儲存 。  
  
4.  若要 **刪除** 現有的自訂記錄層級，可在清單中選取該層級，然後按一下刪除 。  
  
 **自訂記錄層級的權限。**  
  
-   SSISDB 資料庫的所有使用者都能看見自訂的記錄層級，並在執行封裝時，選取自訂的記錄層級。  
  
-   只有 ssis_admin 或 sysadmin 角色的使用者，才可以建立、 更新或刪除自訂的記錄層級。  

## <a name="custom_messages"></a> 自訂訊息以進行記錄
SQL Server Integration Services 提供一組豐富的自訂事件，為套件和許多工作寫入記錄項目。 您可以使用這些項目，透過記錄預先定義事件或使用者自訂訊息，來儲存關於執行進度、結果和問題的詳細資訊，以供稍後分析。 比方說，您可以記錄大量插入開始和結束的時間，以便識別封裝執行時的效能問題。  
  
 自訂記錄項目是一組與可用於封裝以及所有容器和工作的標準記錄事件不同的項目。 自訂記錄項目可以用來擷取與封裝中特定工作相關的有用資訊。 例如，「執行 SQL」工作記錄的其中一個自訂記錄項目會在記錄檔中記錄該工作所執行的 SQL 陳述式。  
  
 所有的記錄項目都包含日期和時間資訊，包括封裝開始和完成時自動寫入的記錄項目。 許多記錄事件都會將多個項目寫入記錄檔。 當事件具有不同的階段時，通常就會發生這種情況。 例如， **ExecuteSQLExecutingQuery** 記錄事件會寫入三個項目：在工作取得資料庫連接之後寫入一個項目、在工作開始準備 SQL 陳述式之後寫入另一個項目，然後在 SQL 陳述式執行完成之後再寫入一個項目。  
  
 下列 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 物件具有自訂記錄項目：  
  
 [封裝](#Package)  
  
 [大量插入工作](#BulkInsert)  
  
 [資料流程工作](#DataFlow)  
  
 [執行 DTS 2000 工作](#ExecuteDTS200)  
  
 [執行處理工作](#ExecuteProcess)  
  
 [執行 SQL 工作](#ExecuteSQL)  
  
 [檔案系統工作](#FileSystem)  
  
 [FTP 工作](#FTP)  
  
 [訊息佇列工作](#MessageQueue)  
  
 [指令碼工作](#Script)  
  
 [傳送郵件工作](#SendMail)  
  
 [傳送資料庫工作](#TransferDatabase)  
  
 [傳輸錯誤訊息工作](#TransferErrorMessages)  
  
 [傳輸作業工作](#TransferJobs)  
  
 [傳輸登入工作](#TransferLogins)  
  
 [傳輸主要預存程序工作](#TransferMasterStoredProcedures)  
  
 [傳送 SQL Server 物件工作](#TransferSQLServerObjects)  
  
 [Web 服務工作](#WebServices)  
  
 [WMI 資料讀取器工作](#WMIDataReader)  
  
 [WMI 事件監看員工作](#WMIEventWatcher)  
  
 [XML 工作](#XML)  
  
### <a name="log-entries"></a>記錄項目  
  
####  <a name="Package"></a> 封裝  
 下表列出封裝的自訂記錄項目。  
  
|記錄項目|說明|  
|---------------|-----------------|  
|**PackageStart**|指出封裝已經開始執行。 此記錄項目會自動寫入記錄檔中。 您無法排除它。|  
|**PackageEnd**|指出封裝已經完成。 此記錄項目會自動寫入記錄檔中。 您無法排除它。|  
|**Diagnostic**|提供影響封裝執行之系統組態的相關資訊，例如可以同時執行的可執行檔數目。<br /><br /> **Diagnostic** 記錄項目也包括呼叫外部資料提供者之前和之後的項目。|  
  
####  <a name="BulkInsert"></a> 大量插入工作  
 下表列出「大量插入」工作的自訂記錄項目。  
  
|記錄項目|說明|  
|---------------|-----------------|  
|**DTSBulkInsertTaskBegin**|指出大量插入已經開始。|  
|**DTSBulkInsertTaskEnd**|指出大量插入已經完成。|  
|**DTSBulkInsertTaskInfos**|提供有關工作的描述性資訊。|  
  
####  <a name="DataFlow"></a> 資料流程工作  
 下表列出「資料流程」工作的自訂記錄項目。  
  
|記錄項目|說明|  
|---------------|-----------------|  
|**BufferSizeTuning**|指出資料流程工作已經變更緩衝區的大小。 記錄項目會描述大小變更的原因，並列出暫存的新緩衝區大小。|  
|**OnPipelinePostEndOfRowset**|表示已經為元件指定了資料列集結尾信號，此信號是由 **ProcessInput** 方法的最後一次呼叫所設定。 處理輸入之資料流程中的每個元件都會寫入一個項目。 項目中包含元件的名稱。|  
|**OnPipelinePostPrimeOutput**|指出元件已經完成 **PrimeOutput** 方法的最後一次呼叫。 根據資料流程而定，可能會寫入多個記錄項目。 如果元件是來源，這表示該元件已經完成處理資料列。|  
|**OnPipelinePreEndOfRowset**|指出元件即將接收其資料列集結尾信號，此信號是由 **ProcessInput** 方法的最後一次呼叫所設定。 處理輸入之資料流程中的每個元件都會寫入一個項目。 項目中包含元件的名稱。|  
|**OnPipelinePrePrimeOutput**|指出元件即將從 **PrimeOutput** 方法接收其呼叫。 根據資料流程而定，可能會寫入多個記錄項目。|  
|**OnPipelineRowsSent**|報告由 **ProcessInput** 方法之呼叫提供給元件輸入的資料列數目。 記錄項目會包含元件名稱。|  
|**PipelineBufferLeak**|提供在緩衝區管理員停止之後使緩衝區保持運作之任何元件的相關資訊。 這表示緩衝區資源並未釋放，而可能導致記憶體遺漏。 記錄項目會提供元件的名稱和緩衝區的識別碼。|  
|**PipelineExecutionPlan**|報告資料流程的執行計畫。 此項目提供如何將緩衝區傳送至元件的相關資訊。 這項資訊結合 PipelineExecutionTrees 項目，描述工作內部所發生的情況。|  
|**PipelineExecutionTrees**|報告資料流程中的配置執行樹狀目錄。 資料流程引擎的排程器使用這些樹狀目錄來建立資料流程的執行計畫。|  
|**PipelineInitialization**|提供有關工作的初始化資訊。 這項資訊包括作為 BLOB 資料暫存儲存位置使用的目錄、預設緩衝區大小，以及緩衝區中的資料列數目。 根據資料流程工作的組態而定，可能會寫入多個記錄項目。|  
  
####  <a name="ExecuteDTS200"></a> 執行 DTS 2000 工作  
 下表列出「執行 DTS 2000」工作的自訂記錄項目。  
  
|記錄項目|說明|  
|---------------|-----------------|  
|**ExecuteDTS80PackageTaskBegin**|指出工作已經開始執行 DTS 2000 封裝。|  
|**ExecuteDTS80PackageTaskEnd**|指出工作已經完成。<br /><br /> 注意：DTS 2000 封裝可能會在工作結束之後繼續執行。|  
|**ExecuteDTS80PackageTaskTaskInfo**|提供有關工作的描述性資訊。|  
|**ExecuteDTS80PackageTaskTaskResult**|報告工作執行之 DTS 2000 封裝的執行結果。|  
  
####  <a name="ExecuteProcess"></a> 執行處理工作  
 下表列出「執行處理」工作的自訂記錄項目。  
  
|記錄項目|說明|  
|---------------|-----------------|  
|**ExecuteProcessExecutingProcess**|提供工作設定執行之可執行檔的執行處理相關資訊。<br /><br /> 將會寫入兩個記錄項目。 其中一個包含工作執行之可執行檔的名稱和位置相關資訊，另一個項目則記錄可執行檔的結束。|  
|**ExecuteProcessVariableRouting**|提供有關哪些變數會傳到可執行檔之輸入和輸出的相關資訊。 將會寫入 stdin (輸入)、stdout (輸出) 和 stderr (錯誤輸出) 的記錄項目。|  
  
####  <a name="ExecuteSQL"></a> 執行 SQL 工作  
 下表描述「執行 SQL」工作的自訂記錄項目。  
  
|記錄項目|說明|  
|---------------|-----------------|  
|**ExecuteSQLExecutingQuery**|提供 SQL 陳述式執行階段的相關資訊。 寫入記錄項目的時機包括在工作取得資料庫連接時、在工作開始準備 SQL 陳述式時，以及在 SQL 陳述式執行完成之後。 準備階段的記錄項目包含工作所使用的 SQL 陳述式。|  
  
####  <a name="FileSystem"></a> 檔案系統工作  
 下表描述「檔案系統」工作的自訂記錄項目。  
  
|記錄項目|說明|  
|---------------|-----------------|  
|**FileSystemOperation**|報告工作執行的作業。 記錄項目會在檔案系統作業開始時寫入，項目中包含有關來源和目的地的資訊。|  
  
####  <a name="FTP"></a> FTP 工作  
 下表列出 FTP 工作的自訂記錄項目。  
  
|記錄項目|說明|  
|---------------|-----------------|  
|**FTPConnectingToServer**|指出工作已經起始與 FTP 伺服器的連接。|  
|**FTPOperation**|報告工作執行之 FTP 作業的開始及其類型。|  
  
####  <a name="MessageQueue"></a> 訊息佇列工作  
 下表列出「訊息佇列」工作的自訂記錄項目。  
  
|記錄項目|說明|  
|---------------|-----------------|  
|**MSMQAfterOpen**|指出工作已經完成開啟訊息佇列。|  
|**MSMQBeforeOpen**|指出工作已經開始開啟訊息佇列。|  
|**MSMQBeginReceive**|指出工作已經開始接收訊息。|  
|**MSMQBeginSend**|指出工作已經開始傳送訊息。|  
|**MSMQEndReceive**|指出工作已經完成接收訊息。|  
|**MSMQEndSend**|指出工作已經完成傳送訊息。|  
|**MSMQTaskInfo**|提供有關工作的描述性資訊。|  
|**MSMQTaskTimeOut**|指出工作已經逾時。|  
  
####  <a name="Script"></a> 指令碼工作  
 下表描述「指令碼」工作的自訂記錄項目。  
  
|記錄項目|說明|  
|---------------|-----------------|  
|**ScriptTaskLogEntry**|報告在指令碼內實作記錄的結果。 每次呼叫 **Log** 物件的 **Dts** 方法時，都會寫入記錄項目。 項目會在程式碼執行時寫入。 如需詳細資訊，請參閱 [Logging in the Script Task](../../integration-services/extending-packages-scripting/task/logging-in-the-script-task.md)。|  
  
####  <a name="SendMail"></a> 傳送郵件工作  
 下表列出「傳送郵件」工作的自訂記錄項目。  
  
|記錄項目|說明|  
|---------------|-----------------|  
|**SendMailTaskBegin**|指出工作已經開始傳送電子郵件訊息。|  
|**SendMailTaskEnd**|指出工作已經完成傳送電子郵件訊息。|  
|**SendMailTaskInfo**|提供有關工作的描述性資訊。|  
  
####  <a name="TransferDatabase"></a> 傳送資料庫工作  
 下表列出「傳送資料庫」工作的自訂記錄項目。  
  
|記錄項目|說明|  
|---------------|-----------------|  
|**SourceDB**|指定工作所複製的資料庫。|  
|**SourceSQLServer**|指定從中複製資料庫的電腦。|  
  
####  <a name="TransferErrorMessages"></a> 傳送錯誤訊息工作  
 下表列出「傳送錯誤訊息」工作的自訂記錄項目。  
  
|記錄項目|說明|  
|---------------|-----------------|  
|**TransferErrorMessagesTaskFinishedTransferringObjects**|指出工作已經完成傳送錯誤訊息。|  
|**TransferErrorMessagesTaskStartTransferringObjects**|指出工作已經開始傳送錯誤訊息。|  
  
####  <a name="TransferJobs"></a> 傳送作業工作  
 下表列出「傳送作業」工作的自訂記錄項目。  
  
|記錄項目|說明|  
|---------------|-----------------|  
|**TransferJobsTaskFinishedTransferringObjects**|指出工作已經完成傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業。|  
|**TransferJobsTaskStartTransferringObjects**|指出工作已經開始傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業。|  
  
####  <a name="TransferLogins"></a> 傳送登入工作  
 下表列出「傳送登入」工作的自訂記錄項目。  
  
|記錄項目|說明|  
|---------------|-----------------|  
|**TransferLoginsTaskFinishedTransferringObjects**|指出工作已經完成傳送登入。|  
|**TransferLoginsTaskStartTransferringObjects**|指出工作已經開始傳送登入。|  
  
####  <a name="TransferMasterStoredProcedures"></a> 傳送主要預存程序工作  
 下表列出「傳送主要預存程序」工作的自訂記錄項目。  
  
|記錄項目|說明|  
|---------------|-----------------|  
|**TransferStoredProceduresTaskFinishedTransferringObjects**|指出工作已經完成傳送儲存在 **master** 資料庫中的使用者定義預存程序。|  
|**TransferStoredProceduresTaskStartTransferringObjects**|指出工作已經開始傳送儲存在 **master** 資料庫中的使用者定義預存程序。|  
  
####  <a name="TransferSQLServerObjects"></a> 傳送 SQL Server 物件工作  
 下表列出「傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件」工作的自訂記錄項目。  
  
|記錄項目|說明|  
|---------------|-----------------|  
|**TransferSqlServerObjectsTaskFinishedTransferringObjects**|指出工作已經完成傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫物件。|  
|**TransferSqlServerObjectsTaskStartTransferringObjects**|指出工作已經開始傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫物件。|  
  
####  <a name="WebServices"></a> Web 服務工作  
 下表列出您可以為「Web 服務」工作啟用的自訂記錄項目。  
  
|記錄項目|Description|  
|---------------|-----------------|  
|**WSTaskBegin**|工作已經開始存取 Web 服務。|  
|**WSTaskEnd**|工作已經完成 Web 服務方法。|  
|**WSTaskInfo**|關於工作的描述性資訊。|  
  
####  <a name="WMIDataReader"></a> WMI 資料讀取器工作  
 下表列出「WMI 資料讀取器」工作的自訂記錄項目。  
  
|記錄項目|說明|  
|---------------|-----------------|  
|**WMIDataReaderGettingWMIData**|指出工作已經開始讀取 WMI 資料。|  
|**WMIDataReaderOperation**|報告工作已執行的 WQL 查詢。|  
  
####  <a name="WMIEventWatcher"></a> WMI 事件監看員工作  
 下表列出「WMI 事件監看員」工作的自訂記錄項目。  
  
|記錄項目|說明|  
|---------------|-----------------|  
|**WMIEventWatcherEventOccurred**|表示發生工作正在監視的事件。|  
|**WMIEventWatcherTimedout**|指出工作已經逾時。|  
|**WMIEventWatcherWatchingForWMIEvents**|指出工作已經開始執行 WQL 查詢。 項目包含查詢。|  
  
####  <a name="XML"></a> XML 工作  
 下表描述 XML 工作的自訂記錄項目。  
  
|記錄項目|說明|  
|---------------|-----------------|  
|**XMLOperation**|提供有關工作執行之作業的資訊。|  

## <a name="related-tasks"></a>相關工作  
 下列清單包含說明如何執行記錄功能相關工作的主題連結。  
  
-   [Integration Services 套件所記錄的事件](../../integration-services/performance/events-logged-by-an-integration-services-package.md)  
  
## <a name="related-content"></a>相關內容  
 [用於完整及詳細記錄的 DTLoggedExec 工具 (CodePlex 專案)](http://go.microsoft.com/fwlink/?LinkId=150579)  

