---
title: SQL Server Compact Edition 連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Compact, connection manager
- connections [Integration Services], SQL Server Compact
- connection managers [Integration Services], SQL Server Compact
ms.assetid: ba627d4d-41f4-49fc-a921-f534cde67770
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4fd067d6f01c168861a42895c36024cb4c0a9aa5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48082788"
---
# <a name="sql-server-compact-edition-connection-manager"></a>SQL Server Compact Edition 連接管理員
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 連線管理員可讓封裝連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 資料庫。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Compact 目的地會使用此連線管理員將資料載入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 資料庫。  
  
> [!NOTE]  
>  在 64 位元電腦上，您必須以 32 位元模式執行連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 資料來源的封裝。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用來連接到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Compact 資料來源的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 提供者只有提供 32 位元版本。  
  
## <a name="configuration-the-sql-server-compact-edition-connection-manager"></a>SQL Server Compact Edition 連接管理員的組態  
 當您將加入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Compact 連接管理員加入封裝時，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]會建立連接管理員，就會解析成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Compact 連接在執行階段，設定連接管理員屬性，並將連接管理員，加入`Connections`封裝上的集合。  
  
 `ConnectionManagerType`連接管理員屬性設定為`SQLMOBILE`。  
  
 您可以利用下列方式設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 連線管理員：  
  
-   提供指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 資料庫位置的連接字串。  
  
-   提供有密碼保護之資料庫的密碼。  
  
-   指定儲存資料庫的伺服器。  
  
-   指示是否在執行階段保留從連接管理員建立的連接。  
  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需有關可以在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [SQL Server Compact Edition 連接管理員編輯器&#40;連接頁面&#41;](../sql-server-compact-edition-connection-manager-editor-connection-page.md)  
  
-   [SQL Server Compact Edition 連接管理員編輯器&#40;所有的頁面&#41;](../sql-server-compact-edition-connection-manager-editor-all-page.md)  
  
 以程式設計方式設定連接管理員的相關資訊，請參閱<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>並[連線以程式設計方式加入](../building-packages-programmatically/adding-connections-programmatically.md)。  
  
  
