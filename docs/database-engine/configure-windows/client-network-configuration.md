---
title: 用戶端網路組態 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- client configuration [SQL Server], connections
- Database Engine [SQL Server], network configurations
- connections [SQL Server], client configuration
- client connections [SQL Server], about client network connections
- client computers [SQL Server]
- client connections [SQL Server]
- network connections [SQL Server], client configuration
ms.assetid: c382eacd-0a0c-40a4-958f-9b774eb2d734
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4fcbb9e6ee0f68433034cd2c3a29f565e05359e9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68012969"
---
# <a name="client-network-configuration"></a>用戶端網路組態
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  用戶端軟體可讓用戶端電腦連接到網路上的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 「用戶端」是前端應用程式，它會使用伺服器 (如 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]) 所提供的服務。 主控這個應用程式的電腦稱為「用戶端電腦」  。  
  
 在最簡單的層級中，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用戶端可以與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體位在相同的機器上。 不過，用戶端通常會透過網路連接到一或多個遠端伺服器。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的用戶端/伺服器架構可供完美無缺地管理網路上的多個用戶端及伺服器。 預設用戶端組態在大部分情況下都會足夠。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用戶端可以包括各種類型的應用程式，例如：  
  
-   OLE DB 取用者  
  
     這些應用程式會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者，連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體。 OLE DB 提供者會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 與把 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料當做 OLE DB 資料列集取用的用戶端應用程式之間居中協調。 **sqlcmd** 命令提示字元公用程式與 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]都是 OLE DB 應用程式的範例。  
  
-   ODBC 應用程式  
  
     這些應用程式包括與舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]一起安裝的用戶端公用程式 (例如 **osql** 命令提示字元公用程式)，以及其他使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的應用程式。  
  
-   DB-Library 用戶端  
  
     這些應用程式包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **isql** 命令提示字元公用程式以及撰寫到 DB-Library 的用戶端。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援用戶端應用程式使用 DB-Library，但僅限於 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 功能。  
  
> [!NOTE]  
>  雖然 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 仍支援使用 DB-Library 和內嵌式 SQL API 的現有應用程式的連接，但它不包含要在使用這些 API 的應用程式上執行程式設計工作所需要的檔案或文件集。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的未來版本將卸除對 DB-Library 或內嵌式 SQL 應用程式連接的支援。 請勿使用 DB-Library 或內嵌式 SQL 來開發新的應用程式。 在修改現有的應用程式時，請移除對 DB-Library 或內嵌式 SQL 的相依性。 如果不想要使用這些 API，請使用 SQLClient 命名空間或 API (例如 OLE DB 或 ODBC)。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不包含執行這些應用程式所需的 DB-Library DLL。 若要執行 DB-Library 或內嵌式 SQL 應用程式，則您必須可從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 版、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 或 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]使用 DB-Library DLL。  
  
 不論應用程式的類型為何，管理用戶端主要在於設定其與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]伺服器元件的連線。 視您站台的需要，用戶端管理的範圍小自輸入伺服器電腦名稱，到建立一個自訂的設定項目以適應多變的多重伺服器環境。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client DLL 包含網路程式庫，而且是透過安裝程式進行安裝。 全新安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]期間不會啟用網路通訊協定。 升級安裝會啟用先前啟用的通訊協定。 基礎網路通訊協定會安裝為 Windows 安裝程式的一部分 (或透過 [控制台] 中的 [網路])。 下列工具可用以管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用戶端：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員  
  
     用戶端與伺服器網路元件都是由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員所管理，其結合了舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 網路公用程式、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用戶端網路公用程式及服務管理員。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員是一個 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console (MMC) 嵌入式管理單元。 它也會以節點形式出現在 Windows Computer Manager 嵌入式管理單元中。 個別的網路程式庫可以使用「 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員」加以啟用、停用、設定及設定優先權。  
  
-   安裝程式  
  
     執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式，將網路元件安裝在用戶端電腦上。 從命令提示字元啟動安裝程式時，可以在安裝期間啟用或停用個別的網路程式庫。  
  
-   ODBC 資料來源管理員  
  
     [ODBC 資料來源管理員] 可讓您在執行 Microsoft Windows 作業系統的電腦上建立及修改 ODBC 資料來源。  
  
## <a name="in-this-section"></a>本節內容  
 [設定用戶端通訊協定](../../database-engine/configure-windows/configure-client-protocols.md)  
  
 [建立或刪除用戶端使用的伺服器別名 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client.md)  
  
 [登入 SQL Server](../../database-engine/configure-windows/logging-in-to-sql-server.md)  
  
 [開啟 ODBC 資料來源管理員](../../database-engine/configure-windows/open-the-odbc-data-source-administrator.md)  
  
 [檢查 ODBC SQL Server 驅動程式版本 &#40;Windows&#41;](../../database-engine/configure-windows/check-the-odbc-sql-server-driver-version-windows.md)  
  
## <a name="related-content"></a>相關內容  
 [伺服器網路組態](../../database-engine/configure-windows/server-network-configuration.md)  
  
 [管理 Database Engine Services](../../database-engine/configure-windows/manage-the-database-engine-services.md)  
  
  
