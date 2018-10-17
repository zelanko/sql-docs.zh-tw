---
title: HTTP 連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- HTTP connection manager
- Web site connections [Integration Services]
- connection managers [Integration Services], HTTP
- Web server connections [Integration Services]
- connections [Integration Services], HTTP
ms.assetid: 26b2b3e1-d02c-46ca-8d31-7aef2bbc3c53
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8b0552d4678df69620d4e97f6f4e1a942dd12330
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48113084"
---
# <a name="http-connection-manager"></a>HTTP 連接管理員
  HTTP 連接讓封裝得以經由使用 HTTP 傳送或接收檔案，存取 Web 伺服器。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 所包含的「Web 服務」工作便使用此連接管理員。  
  
 當您將 HTTP 連接管理員加入封裝時，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會建立連接管理員，用來在執行階段解析為 HTTP 連接、設定連接管理員屬性，以及將連接管理員加入封裝的 `Connections` 集合。  
  
 `ConnectionManagerType`連接管理員屬性設定為 `HTTP.`  
  
 您可以利用下列方式設定 HTTP 連接管理員：  
  
-   使用認證。 如果連接管理員使用認證，其屬性會包含使用者名稱、密碼與網域。  
  
    > [!IMPORTANT]  
    >  HTTP 連接管理員僅支援匿名驗證和基本驗證， 而不支援 Windows 驗證。  
  
-   使用用戶端憑證。 如果連接管理員使用用戶端憑證，其屬性會包含憑證名稱。  
  
-   提供連接到伺服器的逾時以及寫入資料的區塊大小。  
  
-   使用 Proxy 伺服器。 Proxy 伺服器也可設定為使用認證，以及設定為略過 Proxy 伺服器並改用本機位址。  
  
## <a name="configuration-of-the-http-connection-manager"></a>設定 HTTP 連接管理員  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需有關可以在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [HTTP 連接管理員編輯器&#40;伺服器 頁面&#41;](../http-connection-manager-editor-server-page.md)  
  
-   [HTTP 連接管理員編輯器] &#40;[Proxy] 頁面&#41;](../http-connection-manager-editor-proxy-page.md)  
  
 如需以程式設計方式設定連線管理員的資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>。  
  
## <a name="see-also"></a>另請參閱  
 [Web 服務工作](../control-flow/web-service-task.md)   
 [Integration Services &#40;SSIS&#41;連線](integration-services-ssis-connections.md)  
  
  
