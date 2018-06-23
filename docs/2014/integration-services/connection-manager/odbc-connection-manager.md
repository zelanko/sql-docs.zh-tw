---
title: ODBC 連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- connections [Integration Services], ODBC
- ODBC connection manager
- data sources [Integration Services], connections
- connection managers [Integration Services], ODBC
ms.assetid: e8c77aa7-6772-485e-918e-cef9eeb18c58
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 9453dc6e402fce60e1f4f440d84f882e513abea7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36036162"
---
# <a name="odbc-connection-manager"></a>ODBC 連接管理員
  ODBC 連接管理員可使用「開放式資料庫連接 (ODBC)」規格，讓封裝連接到各種資料庫管理系統。  
  
 當您將 ODBC 連接加入封裝並設定連接管理員屬性， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]建立連線管理員，並將連接管理員加入`Connections`封裝的集合。 在執行階段，連接管理員會解析為實體 ODBC 連接。  
  
 `ConnectionManagerType`連接管理員的屬性設定為`ODBC`。  
  
 您可以利用下列方式設定 ODBC 連接管理員：  
  
-   提供參考使用者或系統資料來源名稱的連接字串。  
  
-   指定要連接的伺服器。  
  
-   指示在執行階段是否保留連接。  
  
## <a name="configuration-of-the-odbc-connection-manager"></a>設定 ODBC 連接管理員  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [ODBC 連接管理員 UI 參考](../odbc-connection-manager-ui-reference.md)  
  
 如需以程式設計方式設定連接管理員資訊，請參閱<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>和[新增連線以程式設計方式](../building-packages-programmatically/adding-connections-programmatically.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41;連線](integration-services-ssis-connections.md)  
  
  