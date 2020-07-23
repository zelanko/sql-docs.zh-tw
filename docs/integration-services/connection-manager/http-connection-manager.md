---
title: HTTP 連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.httpconnection.server.f1
- sql13.dts.designer.httpconnection.proxy.f1
helpviewer_keywords:
- HTTP connection manager
- Web site connections [Integration Services]
- connection managers [Integration Services], HTTP
- Web server connections [Integration Services]
- connections [Integration Services], HTTP
ms.assetid: 26b2b3e1-d02c-46ca-8d31-7aef2bbc3c53
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ef8b2df4b24f50f600683a5c6e9bb815208970cc
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86918544"
---
# <a name="http-connection-manager"></a>HTTP 連接管理員

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  HTTP 連接讓封裝得以經由使用 HTTP 傳送或接收檔案，存取 Web 伺服器。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含的「Web 服務」工作會使用此連線管理員。  
  
 當您將 HTTP 連線管理員加入封裝時， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會建立連線管理員，用來在執行階段解析為 HTTP 連接、設定連線管理員屬性，以及將連線管理員加入封裝的 **Connections** 集合。  
  
 連接管理員的 **ConnectionManagerType** 屬性會設定為 **HTTP.** 。  
  
 您可以利用下列方式設定 HTTP 連接管理員：  
  
-   使用認證。 如果連接管理員使用認證，其屬性會包含使用者名稱、密碼與網域。  
  
    > [!IMPORTANT]  
    >  HTTP 連接管理員僅支援匿名驗證和基本驗證， 而不支援 Windows 驗證。  
  
-   使用用戶端憑證。 如果連接管理員使用用戶端憑證，其屬性會包含憑證名稱。  
  
-   提供連接到伺服器的逾時以及寫入資料的區塊大小。  
  
-   使用 Proxy 伺服器。 Proxy 伺服器也可設定為使用認證，以及設定為略過 Proxy 伺服器並改用本機位址。  
  
## <a name="configuration-of-the-http-connection-manager"></a>設定 HTTP 連接管理員  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需以程式設計方式設定連線管理員的資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>。  
  
## <a name="http-connection-manager-editor-server-page"></a>HTTP 連接管理員編輯器 (伺服器頁面)
  使用 [HTTP 連接管理員編輯器] 對話方塊的 [伺服器] 索引標籤指定各項屬性，例如 URL 和安全性認證，以設定 HTTP 連接管理員。 HTTP 連接讓封裝得以經由使用 HTTP 傳送或接收檔案，存取 Web 伺服器。 設定 HTTP 連接管理員之後，可以同時測試連接。  
  
> [!IMPORTANT]  
>  HTTP 連接管理員僅支援匿名驗證和基本驗證， 而不支援 Windows 驗證。  
  
 若要深入了解 HTTP 連接管理員，請參閱＜ [HTTP Connection Manager](../../integration-services/connection-manager/http-connection-manager.md)＞。 若要深入了解 HTTP 連接管理員的常見使用案例，請參閱＜ [Web Service Task](../../integration-services/control-flow/web-service-task.md)＞。  
  
### <a name="options"></a>選項。  
 **伺服器 URL**  
 輸入伺服器的 URL。  
  
 如果您計劃使用 [Web 服務工作編輯器] 中 [一般] 頁面上的 [下載 WSDL] 按鈕來下載 WSDL 檔案，請輸入 WSDL 檔案的 URL。 這個 URL 需以 "?wsdl" 結尾。  
  
 **使用認證**  
 指定 HTTP 連接管理員是否使用使用者的安全性認證進行驗證。  
  
 **使用者名稱**  
 如果 HTTP 連接管理員使用認證，您必須指定使用者名稱、密碼，以及網域。  
  
 **密碼**  
 如果 HTTP 連接管理員使用認證，您必須指定使用者名稱、密碼，以及網域。  
  
 **網域**  
 如果 HTTP 連接管理員使用認證，您必須指定使用者名稱、密碼，以及網域。  
  
 **使用用戶端憑證**  
 指定 HTTP 連接管理員是否使用用戶端憑證進行驗證。  
  
 **[MSSQLSERVER 的通訊協定內容]**  
 使用 [選取憑證]  對話方塊，即可從清單中選取憑證。 文字方塊會顯示與此憑證相關聯的名稱。  
  
 **逾時 (以秒為單位)**  
 提供連接到 Web 伺服器的逾時設定。 此屬性的預設值為 30 秒。  
  
 **區塊大小 (以 KB 為單位)**  
 提供寫入資料的區塊大小。  
  
 **測試連接**  
 設定 HTTP 連接管理員之後，請按一下 [測試連接]  以確認可以看到連接。  
  
## <a name="http-connection-manager-editor-proxy-page"></a>HTTP 連接管理員編輯器 (Proxy 頁面)
  使用 **[HTTP 連接管理員編輯器]** 對話方塊的 **[Proxy]** 索引標籤，來設定 HTTP 連接管理員使用 Proxy 伺服器。 HTTP 連接讓封裝得以經由使用 HTTP 傳送或接收檔案，存取 Web 伺服器。  
  
 若要深入了解 HTTP 連接管理員，請參閱＜ [HTTP Connection Manager](../../integration-services/connection-manager/http-connection-manager.md)＞。 若要深入了解 HTTP 連接管理員的常見使用案例，請參閱＜ [Web Service Task](../../integration-services/control-flow/web-service-task.md)＞。  
  
### <a name="options"></a>選項。  
 **使用 Proxy**  
 指定 HTTP 連接管理員是否要透過 Proxy 伺服器連接。  
  
 **Proxy URL**  
 輸入 Proxy 伺服器的 URL。  
  
 **在本機上略過 Proxy**  
 針對本機位址，指定 HTTP 連接管理員是否要略過 Proxy 伺服器。  
  
 **使用認證**  
 針對 Proxy 伺服器，指定 HTTP 連接管理員是否要使用安全性認證。  
  
 **使用者名稱**  
 如果 HTTP 連接管理員使用認證，您必須指定使用者名稱、密碼，以及網域。  
  
 **密碼**  
 如果 HTTP 連接管理員使用認證，您必須指定使用者名稱、密碼，以及網域。  
  
 **網域**  
 如果 HTTP 連接管理員使用認證，您必須指定使用者名稱、密碼，以及網域。  
  
 **Proxy 略過清單**  
 輸入您想要略過之 Proxy 伺服器的位址清單。  
  
 **加入**  
 輸入您想要針對它略過 Proxy 伺服器的位址。  
  
 **移除**  
 選取一個位址，然後按一下 [移除]  來移除它。  
  
## <a name="see-also"></a>另請參閱  
 [Web 服務工作](../../integration-services/control-flow/web-service-task.md)   
 [Integration Services &#40;SSIS&#41; 連接](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  
