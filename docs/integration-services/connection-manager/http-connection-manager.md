---
title: "HTTP 連接管理員 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "HTTP 連接管理員"
  - "網站連接 [Integration Services]"
  - "連接管理員 [Integration Services], HTTP"
  - "Web 伺服器連接 [Integration Services]"
  - "連接 [Integration Services], HTTP"
ms.assetid: 26b2b3e1-d02c-46ca-8d31-7aef2bbc3c53
caps.latest.revision: 44
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 44
---
# HTTP 連接管理員
  HTTP 連接讓封裝得以經由使用 HTTP 傳送或接收檔案，存取 Web 伺服器。  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 所包含的「Web 服務」工作便使用此連接管理員。  
  
 當您將 HTTP 連線管理員加入封裝時，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會建立連線管理員，用來在執行階段解析為 HTTP 連接、設定連線管理員屬性，以及將連線管理員加入封裝的 **Connections** 集合。  
  
 連接管理員的 **ConnectionManagerType** 屬性會設定為 **HTTP.**。  
  
 您可以利用下列方式設定 HTTP 連接管理員：  
  
-   使用認證。 如果連接管理員使用認證，其屬性會包含使用者名稱、密碼與網域。  
  
    > [!IMPORTANT]  
    >  HTTP 連接管理員僅支援匿名驗證和基本驗證， 而不支援 Windows 驗證。  
  
-   使用用戶端憑證。 如果連接管理員使用用戶端憑證，其屬性會包含憑證名稱。  
  
-   提供連接到伺服器的逾時以及寫入資料的區塊大小。  
  
-   使用 Proxy 伺服器。 Proxy 伺服器也可設定為使用認證，以及設定為略過 Proxy 伺服器並改用本機位址。  
  
## 設定 HTTP 連接管理員  
 您可以透過「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」或以程式設計方式設定屬性。  
  
 如需有關可以在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [HTTP 連線管理員編輯器 &#40;伺服器頁面&#41;](../../integration-services/connection-manager/http-connection-manager-editor-server-page.md)  
  
-   [HTTP 連線管理員編輯器 &#40;Proxy 頁面&#41;](../../integration-services/connection-manager/http-connection-manager-editor-proxy-page.md)  
  
 如需以程式設計方式設定連線管理員的資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>。  
  
## 請參閱＜  
 [Web 服務工作](../../integration-services/control-flow/web-service-task.md)   
 [Integration Services &#40;SSIS&#41; 連接](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  