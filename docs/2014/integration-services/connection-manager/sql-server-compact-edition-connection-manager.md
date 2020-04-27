---
title: SQL Server Compact Edition 連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Compact, connection manager
- connections [Integration Services], SQL Server Compact
- connection managers [Integration Services], SQL Server Compact
ms.assetid: ba627d4d-41f4-49fc-a921-f534cde67770
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 752c825cb34fbf2afe5d2306afbd562a49f74b7f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62833143"
---
# <a name="sql-server-compact-edition-connection-manager"></a>SQL Server Compact Edition 連接管理員
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 連線管理員可讓封裝連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 資料庫。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 包含的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Compact 目的地使用此連線管理員將資料載入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 資料庫中的資料表。  
  
> [!NOTE]  
>  在 64 位元電腦上，您必須以 32 位元模式執行連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 資料來源的封裝。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用來連接到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Compact 資料來源的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 提供者只有提供 32 位元版本。  
  
## <a name="configuration-the-sql-server-compact-edition-connection-manager"></a>SQL Server Compact Edition 連接管理員的組態  
 當您將[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 連線管理員加入封裝時， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]會建立在執行時間解析為[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 連接的連線管理員、設定連線管理員屬性，並將連線管理員加入封裝上`Connections`的集合。  
  
 連接管理員的 `ConnectionManagerType` 屬性會設為 `SQLMOBILE`。  
  
 您可以利用下列方式設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 連線管理員：  
  
-   提供指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 資料庫位置的連接字串。  
  
-   提供有密碼保護之資料庫的密碼。  
  
-   指定儲存資料庫的伺服器。  
  
-   指示是否在執行階段保留從連接管理員建立的連接。  
  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需有關可以在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [SQL Server Compact Edition 連線管理員編輯器 &#40;連接頁面&#41;](../sql-server-compact-edition-connection-manager-editor-connection-page.md)  
  
-   [SQL Server Compact Edition 連線管理員編輯器 &#40;全部頁面&#41;](../sql-server-compact-edition-connection-manager-editor-all-page.md)  
  
 如需以程式設計方式設定連線管理員的資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和 [以程式設計方式加入連接](../building-packages-programmatically/adding-connections-programmatically.md)。  
  
  
