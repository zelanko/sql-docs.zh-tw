---
title: Web 服務工作 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.webservicetask.f1
- sql13.dts.designer.webservicestask.general.f1
- sql13.dts.designer.webservicestask.input.f1
- sql13.dts.designer.webservicestask.output.f1
helpviewer_keywords:
- Web Service task [Integration Services]
ms.assetid: 5c7206f1-7d6a-4923-8dff-3c4912da4157
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f6dde11eba11acc7e0136c34025e74fead99f9e1
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52502611"
---
# <a name="web-service-task"></a>Web 服務工作
  「Web 服務」工作執行一個 Web 服務方法。 您可將「Web 服務」工作用於下列用途：  
  
-   將 Web 服務方法傳回的值寫入變數。 例如，您可以使用 Web 服務方法取得一天的最高溫度，然後使用該值來更新在設定資料行值之運算式中所使用的變數。  
  
-   將 Web 服務方法傳回的值寫入檔案。 例如，可以將潛在客戶清單寫入檔案，該檔案之後將用作封裝中的資料來源，此封裝會在資料寫入資料庫之前清除它們。  
  
## <a name="wsdl-file"></a>WSDL 檔案  
 Web 服務工作使用 HTTP 連接管理員，以連接到 Web 服務。 會在 Web 服務工作以外另行設定 HTTP 連接管理員，然後在工作中參考。 HTTP 連接管理員會指定伺服器 Proxy 設定，例如伺服器 URL、用於存取 Web 服務伺服器的認證以及逾時長度。 如需詳細資訊，請參閱 [HTTP 連線管理員](../../integration-services/connection-manager/http-connection-manager.md)。  
  
> [!IMPORTANT]  
>  HTTP 連接管理員僅支援匿名驗證和基本驗證， 而不支援 Windows 驗證。  
  
 HTTP 連接管理員可指向網站或「Web 服務描述語言」(WSDL) 檔案。 指向 WSDL 檔案之 HTTP 連接管理員的 URL 包含 `?WSDL` 參數：例如 `https://MyServer/MyWebService/MyPage.asmx?WSDL`。  
  
 WSDL 檔案必須可以在本機上使用，這樣才能使用 **設計師提供的 [Web 服務工作編輯器]**[!INCLUDE[ssIS](../../includes/ssis-md.md)] 對話方塊設定 Web 服務工作。  
  
-   如果 HTTP 連接管理員指向網站，則必須手動將 WSDL 檔案複製到本機電腦。  
  
-   如果 HTTP 連接管理員指向 WSDL 檔案，則可透過 Web 服務工作從網站下載該檔案到本機檔案。  
  
 WSDL 檔案會列出 Web 服務提供的方法、方法需要的輸入參數、方法傳回的回應，以及如何與 Web 服務通訊。  
  
 如果方法使用輸入參數，則 Web 服務工作需要參數值。 例如，某個 Web 服務方法依據您的身高建議應購買之滑雪板的長度，則該方法需要在輸入參數中提交您的身高。 參數值可由在工作中定義的字串，或是由在工作或父容器範圍中定義的變數提供。 使用變數的優點就是可讓您利用封裝組態或指令碼，以動態方式更新參數值。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)和[封裝組態](../../integration-services/packages/package-configurations.md)。  
  
 許多 Web 服務方法都不使用輸入參數。 例如，某個 Web 服務方法取得出生於目前月份之總統的姓名，該方法不需要輸入參數，因為 Web 服務可以從本機決定目前月份。  
  
 Web 服務方法的結果可以寫入變數或檔案。 您可以使用「檔案」連接管理員，以指定要寫入結果的檔案或提供要寫入結果的變數名稱。 如需詳細資訊，請參閱[檔案連線管理員](../../integration-services/connection-manager/file-connection-manager.md)和 [Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)。  
  
## <a name="custom-logging-messages-available-on-the-web-service-task"></a>Web 服務工作上可用的自訂記錄訊息  
 下表列出您可以為 Web 服務工作啟用的自訂記錄項目。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 記錄](../../integration-services/performance/integration-services-ssis-logging.md)。  
  
|記錄項目|Description|  
|---------------|-----------------|  
|**WSTaskBegin**|工作已經開始存取 Web 服務。|  
|**WSTaskEnd**|工作已經完成 Web 服務方法。|  
|**WSTaskInfo**|關於工作的描述性資訊。|  
  
## <a name="configuration-of-the-web-service-task"></a>設定 Web 服務工作  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需有關可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中設定之屬性的詳細資訊，請按下列主題：  
  
-   [運算式頁面](../../integration-services/expressions/expressions-page.md)  
  
 如需有關如何在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定這些屬性的詳細資訊，請按下列主題：  
  
-   [設定工作或容器的屬性](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-web-service-task"></a>以程式設計方式設定 Web 服務工作  
 如需有關以程式設計方式設定這些屬性的詳細資訊，請按下列其中一個主題：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.WebServiceTask.WebServiceTask>  
  
## <a name="web-service-task-editor-general-page"></a>Web 服務工作編輯器 (一般頁面)
  使用 [Web 服務工作編輯器] 對話方塊的 [一般] 頁面，來指定 HTTP 連接管理員、指定 Web 服務工作使用的 Web 服務描述語言 (WSDL) 檔案的位置、描述 Web 服務工作，以及下載 WSDL 檔案。  
  
### <a name="options"></a>選項。  
 **HTTPConnection**  
 在清單中選取連線管理員，或按一下 [\<新增連線...>] 建立新的連線管理員。  
  
> [!IMPORTANT]  
>  HTTP 連接管理員僅支援匿名驗證和基本驗證， 而不支援 Windows 驗證。  
  
 **相關主題：**[HTTP 連接管理員](../../integration-services/connection-manager/http-connection-manager.md)、[HTTP 連接管理員編輯器 &#40;伺服器頁面&#41;](../../integration-services/connection-manager/http-connection-manager-editor-server-page.md)  
  
 **WSDLFile**  
 鍵入本機電腦的 WSDL 檔案完整路徑，或按一下瀏覽按鈕 **(...)** 並找出此檔案。  
  
 如果您已經將 WSDL 檔案手動下載到電腦中，請選取該檔案。 如果尚未下載 WSDL 檔案，則請執行下列步驟：  
  
-   建立副檔名為 ".wsdl" 的空白檔案。  
  
-   在 [WSDLFile] 選項中選取此空白檔案。  
  
-   將 **OverwriteWSDLFile** 的值設為 [True]，讓實際的 WSDL 檔案可以覆寫此空白檔案。  
  
-   按一下 [下載 WSDL]，下載實際的 WSDL 檔案並覆寫空白檔案。  
  
    > [!NOTE]  
    >  您必須先在 [WSDLFile] 方塊中提供現有的本機檔案名稱，才能啟用 [下載 WSDL] 選項。  
  
 **OverwriteWSDLFile**  
 指出是否可以覆寫 Web 服務工作的 WSDL 檔案。  
  
 如果您想要使用 [下載 WSDL] 按鈕來下載 WSDL檔案，請將此值設為 [True]。  
  
 **名稱**  
 為 Web 服務工作提供唯一的名稱。 這個名稱是作為工作圖示中的標籤使用。  
  
> [!NOTE]  
>  工作名稱在封裝內必須是唯一的。  
  
 **說明**  
 輸入 Web 服務工作的描述。  
  
 **下載 WSDL**  
 下載 WSDL 檔案。  
  
 您必須先在 [WSDLFile] 方塊中提供現有的本機檔案名稱，才能啟用此按鈕。  
  
## <a name="web-service-task-editor-input-page"></a>Web 服務工作編輯器 (輸入頁面)
  使用 [Web 服務工作編輯器] 對話方塊的 [輸入] 頁面，即可指定 Web 服務、Web 方法，以及提供給 Web 方法的輸入值。 在 [值] 資料行中直接輸入字串，或是在 [值] 資料行中選取變數，即可提供這些值。  
  
### <a name="options"></a>選項。  
 **服務**  
 從清單中選取要用於執行 Web 方法的 Web 服務。  
  
 **方法**  
 從清單中選取要用於執行工作的 Web 方法。  
  
 **WebMethodDocumentation**  
 鍵入 Web 方法的描述，或按一下瀏覽按鈕 **(...)**，然後在 [Web 方法文件集] 對話方塊中鍵入描述。  
  
 **名稱**  
 列出 Web 方法之輸入的名稱。  
  
 **型別**  
 列出輸入的資料類型。  
  
> [!NOTE]  
>  「Web 服務」工作只支援下列資料類型的參數：基本類型 (如整數和字串)、基本類型的陣列和順序以及列舉。  
  
 **變數**  
 選取該核取方塊，即可使用變數來提供輸入。  
  
 **ReplTest1**  
 如果選取了 [變數] 核取方塊，請從清單中選取要用於提供輸入的變數，否則請直接輸入要用於輸入的值。  
  
## <a name="web-service-task-editor-output-page"></a>Web 服務工作編輯器 (輸出頁面)
  使用 [Web 服務工作編輯器] 對話方塊的 [輸出] 頁面，即可指定 Web 方法傳回的結果之儲存位置。  
  
### <a name="static-options"></a>靜態選項  
 **OutputType**  
 選取儲存結果時使用的儲存類型。 這個屬性具有下表中所列的選項。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**檔案連接**|在檔案中儲存結果。 選取此值會顯示動態選項 [檔案]。|  
|**變數**|在變數中儲存結果。 選取此值會顯示動態選項 [變數]。|  
  
### <a name="outputtype-dynamic-options"></a>OutputType 動態選項  
  
#### <a name="outputtype--file-connection"></a>OutputType = 檔案連接  
 **檔案**  
 在清單中選取檔案連線管理員，或按一下 [\<新增連線...>] 建立新的連線管理員。  
  
 **相關主題：** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)、 [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
#### <a name="outputtype--variable"></a>OutputType = 變數  
 **變數**  
 在清單中選取變數，或按一下 [\<新增變數...>] 建立新的變數。  
  
 **相關主題：**[Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)、[新增變數](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
## <a name="related-content"></a>相關內容  
 technet.microsoft.com 上的影片： [How to: Call a Web Service by Using the Web Service Task](https://go.microsoft.com/fwlink/?LinkId=259642)(如何：使用 Web 服務工作呼叫 Web 服務) (SQL Server 影片)。  
