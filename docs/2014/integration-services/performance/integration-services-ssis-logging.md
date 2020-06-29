---
title: Integration Services (SSIS) 記錄 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
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
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 30f65b7bfd4563bbc9ada1d615f0d48af225895d
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85423405"
---
# <a name="integration-services-ssis-logging"></a>Integration Services (SSIS) 記錄
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包括可用於在套件、容器和工作中實作記錄的記錄提供者。 使用記錄，可以擷取有關封裝的執行階段資訊，藉此幫助您在每次執行封裝時對其進行稽核和疑難排解。 例如，記錄可以擷取執行封裝之操作員的名稱，以及封裝開始和結束的時間。  
  
 您可以設定在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器上的封裝執行期間發生的記錄範圍。 如需詳細資訊，請參閱 [在 SSIS 伺服器上啟用封裝執行的記錄功能](../enable-logging-for-package-execution-on-the-ssis-server.md)。  
  
 您還可以在使用 **dtexec** 命令提示公用程式執行封裝時，併入記錄功能。 如需支援記錄功能之命令提示引數的詳細資訊，請參閱 [dtexec 公用程式](../packages/dtexec-utility.md)。  
  
## <a name="configure-logging-in-sql-server-data-tools"></a>設定 SQL Server Data Tools 中的記錄功能  
 記錄與封裝相關聯，並在封裝層級設定。 封裝中的每個工作或容器都可將資訊記錄至任何封裝記錄檔中。 您可以啟用封裝中工作和容器的記錄功能，即使該封裝本身未啟用記錄功能。 例如，可以在「執行 SQL」工作上啟用記錄功能，而無需在父封裝上啟用記錄功能。 封裝、容器或工作可以寫入多重記錄檔。 您可以僅在封裝上啟用記錄功能，也可以選擇在封裝所包含的任何個別工作或容器上啟用記錄功能。  
  
 當您將記錄加入封裝時，請選擇記錄提供者和記錄的位置。 記錄提供者會指定記錄資料的格式：例如， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫或文字檔。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包括下列記錄提供者：  
  
-   「文字檔」記錄提供者，它會將記錄項目以逗號分隔值 (CSV) 的格式寫入 ASCII 文字檔。 此提供者的預設副檔名為 .log。  
  
-   [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 記錄提供者，它可寫入追蹤檔，您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler 檢視該追蹤檔。 此提供者的預設副檔名為 .trc。  
  
    > [!NOTE]  
    >  您無法在以 64 位元模式執行的封裝中使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 記錄提供者。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]記錄提供者，它會將記錄專案寫入 `sysssislog` 資料庫中的資料表 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
-   「Windows 事件」記錄提供者，它可將項目寫入本機電腦上之「Windows 事件」記錄的「應用程式」記錄中。  
  
-   「XML 檔案」記錄提供者，它可將記錄檔寫入 XML 檔案中。 此提供者的預設副檔名為 .xml。  
  
 如果您將記錄提供者加入封裝或以程式設計的方式設定記錄，則可以使用 ProgID 或 ClassID 來識別記錄提供者，以取代使用 [設定 SSIS 記錄] 對話方塊中所顯示之 [[!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師] 的名稱。  
  
 下表列出 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 所包含之記錄提供者的 ProgID 和 ClassID，以及記錄提供者寫入記錄檔的位置。  
  
|記錄提供者|ProgID|ClassID|Location|  
|------------------|------------|-------------|--------------|  
|文字檔|DTS.LogProviderTextFile|{0A039101-ACC1-4E06-943F-279948323883}|記錄提供者所使用的「檔案」連接管理員會指定文字檔的路徑。|  
|SQL Server Profiler|DTS.LogProviderSQLProfiler|{E93F6300-AE0C-4916-A7BF-A8D0CE12C77A}|記錄提供者所使用的「檔案」連線管理員會指定 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]所使用之檔案的路徑。|  
|SQL Server|DTS.LogProviderSQLServer|{94150B25-6AEB-4C0D-996D-D37D1C4FDEDA}|記錄提供者所使用的 OLE DB 連線管理員會指定包含具有記錄項目之 sysssislog 資料表的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。|  
|Windows 事件記錄檔|DTS.LogProviderEventLog|{071CC8EB-C343-4CFF-8D58-564B92FCA3CF}|Windows 事件檢視器中的應用程式記錄檔包含 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 記錄資訊。|  
|XML 檔案|DTS.LogProviderXMLFile|{440945A4-2A22-4F19-B577-EAF5FDDC5F7A}|記錄提供者所使用的「檔案」連接管理員會指定 XML 檔案的路徑。|  
  
 您還可以建立自訂記錄提供者。 如需詳細資訊，請參閱 [建立自訂記錄提供者](../extending-packages-custom-objects/log-provider/creating-a-custom-log-provider.md)。  
  
 封裝中的記錄提供者是此封裝之記錄提供者集合的成員。 使用 [[!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師] 建立封裝並實作記錄時，您可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師的 [封裝總管] 索引標籤上，看到 [記錄提供者] 資料夾中集合成員的清單。  
  
 您可以藉由提供記錄提供者的名稱和描述，並指定記錄提供者使用的連接管理員，來設定記錄提供者。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記錄提供者會使用 OLE DB 連接管理員。 「文字檔」、「 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]」和「XML 檔案」記錄提供者全都使用「檔案」連線管理員。 Windows 事件記錄檔提供者不使用連接管理員，因為它會直接寫入「Windows 事件記錄檔」中。 如需詳細資訊，請參閱 [OLE DB 連線管理員](../connection-manager/ole-db-connection-manager.md) 和 [檔案連線管理員](../connection-manager/file-connection-manager.md)。  
  
### <a name="logging-customization"></a>自訂記錄  
 為了自訂事件或自訂訊息的記錄， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供通常記錄之資訊的結構描述，以用於併入記錄項目。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 記錄結構描述會定義可以記錄的資訊。 您可以從記錄結構描述選擇每個記錄項目的元素。  
  
 封裝及其容器和工作不一定要記錄相同資訊，相同封裝或容器內的工作也可以記錄不同的資訊。 例如，封裝可以在封裝啟動時記錄操作員資訊，一個工作可以記錄工作失敗的來源，而另一個工作可以在發生錯誤時記錄資訊。 如果封裝及其容器和工作使用多重記錄檔，則相同的資訊會寫入所有記錄檔中。  
  
 您可以指定要記錄的事件和每個事件要記錄的資訊，以選取符合您需要的記錄層級。 您可能會發現某些事件提供的資訊比其他事件更有用。 例如，您可能只想記錄 **PreExecute** 事件的電腦和操作員名稱，而不是 **Error** 事件的所有可用資訊。  
  
 若要防止記錄檔使用大量的磁碟空間，或避免可能會降低效能的過度記錄，可以選取要記錄的特定事件和資訊項目，以限制記錄。 例如，您可以設定記錄檔僅擷取每個錯誤的日期和電腦名稱。  
  
 在 [[!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師] 中，使用 [設定 SSIS 記錄]  對話方塊來定義記錄選項。  
  
#### <a name="log-schema"></a>記錄結構描述  
 下表描述記錄結構描述中的元素。  
  
|元素|描述|  
|-------------|-----------------|  
|電腦|發生記錄事件之電腦的名稱。|  
|運算子|啟動封裝之使用者的識別。|  
|SourceName|發生記錄事件之容器或工作的名稱。|  
|SourceID|封裝的唯一識別碼；「For 迴圈」、「Foreach 迴圈」或「時序」容器；或者發生記錄事件的工作。|  
|ExecutionID|封裝執行執行個體的 GUID。<br /><br /> 請注意：執行單一封裝可能會建立記錄項目，其中包含不同的 ExecutionID 元素值。 例如，當您在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中執行封裝時，驗證階段可能會建立記錄項目，其中包含了對應到 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]的 ExecutionID 元素。 但是，執行階段可能會建立記錄項目，其中包含了對應到 dtshost.exe 的 ExecutionID 元素。 在另一個範例中，當您執行包含「執行封裝」工作的封裝時，每一個工作都會執行子封裝。 這些子封裝可能會建立記錄項目，其中包含了與父封裝建立之記錄項目不同的 ExecutionID 元素。|  
|MessageText|與記錄項目相關聯的訊息。|  
|DataBytes|記錄項目特定的位元組陣列。 此欄位的意義會因記錄項目的不同而不同。|  
  
 下表描述記錄結構描述中，在 [設定 SSIS 記錄] 對話方塊的 [詳細資料] 索引標籤上沒有提供的三個額外元素。  
  
|元素|描述|  
|-------------|-----------------|  
|StartTime|容器或工作開始執行的時間。|  
|EndTime|容器或工作停止執行的時間。|  
|DataCode|選擇性的整數值，一般會包含 <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult> 列舉的值，指出執行容器或工作的結果：<br /><br /> 0 - 成功<br /><br /> 1 - 失敗<br /><br /> 2 - 已完成<br /><br /> 3 - 已取消|  
  
##### <a name="log-entries"></a>記錄項目  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 支援預先定義事件上的記錄項目，並為許多 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 物件提供自訂記錄項目。 在 [[!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師] 中的 [設定 SSIS 記錄] 對話方塊會列出這些事件和自訂記錄項目。  
  
 下表描述的預先定義事件可在發生執行階段事件時寫入記錄項目。 這些記錄項目會套用至可執行檔、封裝和封裝所包含的工作和容器。 記錄項目的名稱與引發並造成寫入記錄項目之執行階段事件的名稱相同。  
  
|事件|描述|  
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
|**Diagnostic**|寫入提供診斷資訊的記錄項目。<br /><br /> 例如，您可以在每次呼叫外部資料提供者前後記錄訊息。 如需詳細資訊，請參閱 [封裝執行的疑難排解工具](../troubleshooting/troubleshooting-tools-for-package-execution.md)。|  
  
 封裝及許多工作都有可以啟用記錄功能的自訂記錄項目。 例如，[傳送郵件] 工作會提供 **SendMailTaskBegin** 自訂記錄項目，其會在 [傳送郵件] 工作開始執行時，但在工作傳送電子郵件訊息之前，記錄資訊。 如需詳細資訊，請參閱[自訂訊息以進行記錄](../custom-messages-for-logging.md)。  
  
### <a name="differentiating-package-copies"></a>區分封裝副本  
 記錄資料包含記錄項目所屬封裝的名稱和 GUID。 如果您透過複製現有的封裝來建立新的封裝，將一併複製現有封裝的名稱和 GUID。 因此，您可能會有兩套具有相同 GUID 和名稱的封裝，使您難以區分記錄資料中的封裝。  
  
 為了消除這種模糊不清的狀況，您應該更新這個新封裝的名稱和 GUID。 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中，您可以在 [屬性] 視窗的 `ID` 屬性中重新產生 GUID，並更新 `Name` 屬性的值。 您也可以使用程式設計方式或 **dtutil** 命令提示字元來變更 GUID 和名稱。 如需詳細資訊，請參閱 [設定封裝屬性](../set-package-properties.md) 和 [dtutil 公用程式](../dtutil-utility.md)。  
  
### <a name="parent-logging-options"></a>父記錄選項  
 通常，工作和「For 迴圈」、「Foreach 迴圈」和「時序」容器的記錄選項符合封裝或父容器的選項。 在該情況下，可以設定它們從其父容器繼承記錄選項。 例如，在包含「執行 SQL」工作的「For 迴圈」容器中，「執行 SQL」工作可以使用在「For 迴圈」容器上設定的記錄選項。 若要使用父記錄選項，可將容器的 LoggingMode 屬性設為 **UseParentSetting**。 可以在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 的 [屬性]**** 視窗中，或透過 [[!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師] 的 [設定 SSIS 記錄]**** 對話方塊設定此屬性。  
  
### <a name="logging-templates"></a>記錄範本  
 在 [設定 SSIS 記錄]**** 對話方塊中，還可以將常用的記錄組態建立和儲存為範本，然後在多個封裝中使用這些範本。 這使得跨多個封裝套用一致的記錄策略，以及修改封裝的記錄設定變得很容易，只要更新後再套用範本即可。 範本以 XML 檔案儲存。  
  
 **若要使用 [設定 SSIS 記錄] 對話方塊設定記錄**  
  
1.  啟用封裝及其工作的記錄功能。 記錄可以發生在封裝、容器和工作層級上。 您可以為封裝、容器和工作指定不同的記錄檔。  
  
2.  選取記錄提供者，並為封裝加入記錄。 記錄檔僅可以在封裝層級建立，且工作或容器必須使用為封裝建立的記錄檔之一。 每個記錄檔都與下列記錄提供者之一相關聯：文字檔、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、Windows 記錄檔或 XML 檔案。 如需詳細資訊，請參閱 [在 SQL Server Data Tools 中啟用封裝記錄功能](../enable-package-logging-in-sql-server-data-tools.md)。  
  
3.  選取事件，以及要在記錄檔中擷取之每個事件的記錄結構描述資訊。 如需詳細資訊，請參閱 [使用已儲存的組態檔來設定記錄](../configure-logging-by-using-a-saved-configuration-file.md)。  
  
### <a name="configuration-of-log-provider"></a>設定記錄提供者  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 記錄提供者是按照在封裝中實作記錄的步驟而建立和設定的。 如需詳細資訊，請參閱[Integration Services 記錄](integration-services-ssis-logging.md)。  
  
 建立記錄提供者之後，您可以在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]的 [屬性] 視窗中檢視和修改其屬性。  
  
 如需以程式設計方式設定這些屬性的詳細資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider> 類別的文件。  
  
### <a name="logging-for-data-flow-tasks"></a>資料流程工作的記錄功能  
 資料流程工作提供許多可用以監視及調整效能的自訂記錄項目。 例如，您可以監視可能會造成記憶體遺漏的元件，或是追蹤執行某特定元件所花費的時間。 如需這些自訂記錄項目的清單以及記錄輸出範例，請參閱 [資料流程工作](../control-flow/data-flow-task.md)。  
  
#### <a name="use-the-pipelinecomponenttime-event"></a>使用 PipelineComponentTime 事件  
 最有用的自訂記錄項目可能是 PipelineComponentTime 事件。 這個記錄項目會報告每個元件在五個主要處理步驟的每個步驟中所花費的毫秒數。 下表描述這些處理步驟。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 開發人員會將這些步驟辨識為 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>。  
  
|步驟|描述|  
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
  
## <a name="related-tasks"></a>相關工作  
 下列清單包含說明如何執行記錄功能相關工作的主題連結。  
  
-   [設定 SSIS 記錄對話方塊](../configure-ssis-logs-dialog-box.md)  
  
-   [在 SQL Server Data Tools 中啟用封裝記錄功能](../enable-package-logging-in-sql-server-data-tools.md)  
  
-   [在 SSIS 伺服器上啟用封裝執行的記錄功能](../enable-logging-for-package-execution-on-the-ssis-server.md)  
  
-   [檢視記錄事件視窗中的記錄項目](../view-log-entries-in-the-log-events-window.md)  
  
## <a name="related-content"></a>相關內容  
 [用於完整及詳細記錄的 DTLoggedExec 工具 (CodePlex 專案)](https://go.microsoft.com/fwlink/?LinkId=150579)  
  
## <a name="see-also"></a>另請參閱  
 [檢視記錄事件視窗中的記錄項目](../view-log-entries-in-the-log-events-window.md)  
  
  
