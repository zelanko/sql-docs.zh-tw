---
title: HTTP 連接管理員編輯器 （伺服器頁面） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.httpconnection.server.f1
helpviewer_keywords:
- HTTP Connection Manager Editor
ms.assetid: 774778a0-ece6-4971-b93f-b121d8fc1fc1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 197a2668beb60acf2473a1f53786d7b553e08cf6
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66058248"
---
# <a name="http-connection-manager-editor-server-page"></a>HTTP 連接管理員編輯器 (伺服器頁面)
  使用 [HTTP 連接管理員編輯器] 對話方塊的 [伺服器] 索引標籤指定各項屬性，例如 URL 和安全性認證，以設定 HTTP 連接管理員。 HTTP 連接讓封裝得以經由使用 HTTP 傳送或接收檔案，存取 Web 伺服器。 設定 HTTP 連接管理員之後，可以同時測試連接。  
  
> [!IMPORTANT]  
>  HTTP 連接管理員僅支援匿名驗證和基本驗證， 而不支援 Windows 驗證。  
  
 若要深入了解 HTTP 連接管理員，請參閱＜ [HTTP Connection Manager](connection-manager/http-connection-manager.md)＞。 若要深入了解 HTTP 連接管理員的常見使用案例，請參閱＜ [Web Service Task](control-flow/web-service-task.md)＞。  
  
## <a name="options"></a>選項。  
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
 使用 [選取憑證] 對話方塊，即可從清單中選取憑證。 文字方塊會顯示與此憑證相關聯的名稱。  
  
 **逾時 (以秒為單位)**  
 提供連接到 Web 伺服器的逾時設定。 此屬性的預設值為 30 秒。  
  
 **區塊大小 (以 KB 為單位)**  
 提供寫入資料的區塊大小。  
  
 **測試連接**  
 設定 HTTP 連接管理員之後，請按一下 [測試連接] 以確認可以看到連接。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [HTTP 連接管理員編輯器 &#40;Proxy 頁面&#41;](../../2014/integration-services/http-connection-manager-editor-proxy-page.md)  
  
  
