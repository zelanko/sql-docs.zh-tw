---
title: "ODBC 連接管理員 | Microsoft Docs"
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
  - "連接 [Integration Services], ODBC"
  - "ODBC 連接管理員"
  - "資料來源 [Integration Services], 連接"
  - "連接管理員 [Integration Services], ODBC"
ms.assetid: e8c77aa7-6772-485e-918e-cef9eeb18c58
caps.latest.revision: 41
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 41
---
# ODBC 連接管理員
  ODBC 連接管理員可使用「開放式資料庫連接 (ODBC)」規格，讓封裝連接到各種資料庫管理系統。  
  
 當您將 ODBC 連接加入封裝並設定連線管理員屬性時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會建立連線管理員，並將該連線管理員加入到封裝的 **Connections** 集合。 在執行階段，連接管理員會解析為實體 ODBC 連接。  
  
 連線管理員的 **ConnectionManagerType** 屬性會設為 **ODBC**。  
  
 您可以利用下列方式設定 ODBC 連接管理員：  
  
-   提供參考使用者或系統資料來源名稱的連接字串。  
  
-   指定要連接的伺服器。  
  
-   指示在執行階段是否保留連接。  
  
## 設定 ODBC 連接管理員  
 您可以透過「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」或以程式設計方式設定屬性。  
  
 如需可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [ODBC 連接管理員 UI 參考](../../integration-services/connection-manager/odbc-connection-manager-ui-reference.md)  
  
 如需以程式設計方式設定連線管理員的相關資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和[以程式設計方式加入連接](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)。  
  
## 請參閱＜  
 [Integration Services &#40;SSIS&#41; 連接](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  