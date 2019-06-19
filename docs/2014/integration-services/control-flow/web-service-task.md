---
title: Web 服務工作 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.webservicetask.f1
helpviewer_keywords:
- Web Service task [Integration Services]
ms.assetid: 5c7206f1-7d6a-4923-8dff-3c4912da4157
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f21a5f938b2dcd7b90fa71ab946d2986b0633987
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62829408"
---
# <a name="web-service-task"></a>Web 服務工作
  「Web 服務」工作執行一個 Web 服務方法。 您可將「Web 服務」工作用於下列用途：  
  
-   將 Web 服務方法傳回的值寫入變數。 例如，您可以使用 Web 服務方法取得一天的最高溫度，然後使用該值來更新在設定資料行值之運算式中所使用的變數。  
  
-   將 Web 服務方法傳回的值寫入檔案。 例如，可以將潛在客戶清單寫入檔案，該檔案之後將用作封裝中的資料來源，此封裝會在資料寫入資料庫之前清除它們。  
  
## <a name="wsdl-file"></a>WSDL 檔案  
 Web 服務工作使用 HTTP 連接管理員，以連接到 Web 服務。 會在 Web 服務工作以外另行設定 HTTP 連接管理員，然後在工作中參考。 HTTP 連接管理員會指定伺服器 Proxy 設定，例如伺服器 URL、用於存取 Web 服務伺服器的認證以及逾時長度。 如需詳細資訊，請參閱 [HTTP 連線管理員](../connection-manager/http-connection-manager.md)。  
  
> [!IMPORTANT]  
>  HTTP 連接管理員僅支援匿名驗證和基本驗證， 而不支援 Windows 驗證。  
  
 HTTP 連接管理員可指向網站或「Web 服務描述語言」(WSDL) 檔案。 指向 WSDL 檔案之 HTTP 連接管理員的 URL 包含 `?WSDL` 參數：例如 `http://MyServer/MyWebService/MyPage.asmx?WSDL`。  
  
 WSDL 檔案必須可以在本機上使用，這樣才能使用 **設計師提供的 [Web 服務工作編輯器]** [!INCLUDE[ssIS](../../includes/ssis-md.md)] 對話方塊設定 Web 服務工作。  
  
-   如果 HTTP 連接管理員指向網站，則必須手動將 WSDL 檔案複製到本機電腦。  
  
-   如果 HTTP 連接管理員指向 WSDL 檔案，則可透過 Web 服務工作從網站下載該檔案到本機檔案。  
  
 WSDL 檔案會列出 Web 服務提供的方法、方法需要的輸入參數、方法傳回的回應，以及如何與 Web 服務通訊。  
  
 如果方法使用輸入參數，則 Web 服務工作需要參數值。 例如，某個 Web 服務方法依據您的身高建議應購買之滑雪板的長度，則該方法需要在輸入參數中提交您的身高。 參數值可由在工作中定義的字串，或是由在工作或父容器範圍中定義的變數提供。 使用變數的優點就是可讓您利用封裝組態或指令碼，以動態方式更新參數值。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 變數](../integration-services-ssis-variables.md)和[封裝組態](../package-configurations.md)。  
  
 許多 Web 服務方法都不使用輸入參數。 例如，某個 Web 服務方法取得出生於目前月份之總統的姓名，該方法不需要輸入參數，因為 Web 服務可以從本機決定目前月份。  
  
 Web 服務方法的結果可以寫入變數或檔案。 您可以使用「檔案」連接管理員，以指定要寫入結果的檔案或提供要寫入結果的變數名稱。 如需詳細資訊，請參閱[檔案連線管理員](../connection-manager/file-connection-manager.md)和 [Integration Services &#40;SSIS&#41; 變數](../integration-services-ssis-variables.md)。  
  
## <a name="custom-logging-messages-available-on-the-web-service-task"></a>Web 服務工作上可用的自訂記錄訊息  
 下表列出您可以為 Web 服務工作啟用的自訂記錄項目。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 記錄](../performance/integration-services-ssis-logging.md)和[自訂訊息以進行記錄](../custom-messages-for-logging.md)。  
  
|記錄項目|描述|  
|---------------|-----------------|  
|`WSTaskBegin`|工作已經開始存取 Web 服務。|  
|`WSTaskEnd`|工作已經完成 Web 服務方法。|  
|`WSTaskInfo`|關於工作的描述性資訊。|  
  
## <a name="configuration-of-the-web-service-task"></a>設定 Web 服務工作  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需有關可以在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [Web 服務工作編輯器 &#40;[一般] 頁面&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Web 服務工作編輯器 &#40;[輸入] 頁面&#41;](../web-service-task-editor-input-page.md)  
  
-   [Web 服務工作編輯器 &#40;[輸出] 頁面&#41;](../web-service-task-editor-output-page.md)  
  
-   [運算式頁面](../expressions/expressions-page.md)  
  
 如需有關如何在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定這些屬性的詳細資訊，請按下列主題：  
  
-   [設定工作或容器的屬性](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-the-web-service-task"></a>以程式設計方式設定 Web 服務工作  
 如需有關以程式設計方式設定這些屬性的詳細資訊，請按下列其中一個主題：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.WebServiceTask.WebServiceTask>  
  
## <a name="related-content"></a>相關內容  
 影片，[如何：technet.microsoft.com 上的影片：使用 Web 服務工作呼叫 Web 服務) (SQL Server 影片)](https://go.microsoft.com/fwlink/?LinkId=259642) \(英文\)。  
  
 [如何使用 Web 服務，透過 SSIS 套件](https://www.c-sharpcorner.com/article/how-to-consume-web-service-through-ssis-package/)。  
  
  
