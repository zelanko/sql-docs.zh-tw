---
title: RDS 使用 ODBC 連接共用 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connection pooling in RDS [ADO]
ms.assetid: e8b912c1-da5b-4e85-a000-1e6648a94237
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 14f06b98896a63f8e19ce22fb9cd1eb5b181f481
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66699256"
---
# <a name="using-rds-with-odbc-connection-pooling"></a>搭配 ODBC 連線集區使用 RDS
如果您使用 ODBC 資料來源，您可以使用連接共用選項在網際網路資訊服務 (IIS)，以達到高效能處理的用戶端負載。 連接共用是資源管理員的連接，維護常用的連接上的 [開啟] 狀態。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 若要啟用連線共用，請參閱 Internet Information Services 文件。  
  
 請注意，啟用連線共用可能會遵守 Web 伺服器的其他限制，Microsoft Internet Information Services 文件中所述。  
  
 若要確保，連接共用是穩定，並提供進一步提高效能，您必須設定 Microsoft SQL Server 以使用 TCP/IP 通訊端通訊協定網路程式庫。  
  
 若要這樣做，您需要：  
  
-   設定 SQL Server 電腦使用 TCP/IP 通訊端。  
  
-   設定 Web 伺服器使用 TCP/IP Sockets。  
  
## <a name="configuring-the-sql-server-computer-to-use-tcpip-sockets"></a>設定 SQL Server 電腦使用 TCP/IP 通訊端  
 SQL Server 電腦上，執行 SQL Server 安裝程式，以便與資料來源的互動所使用的 TCP/IP 通訊端網路程式庫。  
  
### <a name="to-specify-the-tcpip-socket-network-library-on-the-sql-server-computer"></a>若要指定 SQL Server 電腦上的 TCP/IP 通訊端通訊協定網路程式庫  
  
### <a name="in-microsoft-sql-server-65"></a>在 Microsoft SQL Server 6.5 中：  
  
1.  從 開始 功能表中，指向 程式、 指向 Microsoft SQL Server 6.5、，然後按一下 SQL 安裝程式。  
  
2.  按一下 繼續兩次。  
  
3.  Microsoft SQL Server 中的選項] 對話方塊中，選取 [變更網路支援，，然後按一下 [繼續]。  
  
4.  請確定已選取 TCP/IP 通訊端 核取方塊，並按一下 確定。  
  
5.  按一下 [繼續] 來完成，並結束安裝程式。  
  
### <a name="in-microsoft-sql-server-70"></a>在 Microsoft SQL Server 7.0:  
  
1.  從 開始 功能表中，指向 程式、 指向 Microsoft SQL Server 7.0、，然後按一下伺服器網路公用程式。  
  
2.  在對話方塊中 [一般] 索引標籤中，按一下 [新增]。  
  
3.  在 加入網路程式庫組態 對話方塊中，按一下 TCP/IP。  
  
4.  在連接埠號碼和 Proxy 位址方塊中，輸入您的網路系統管理員所提供的連接埠號碼和 proxy 位址。  
  
5.  按一下 [確定] 完成，並結束安裝程式。  
  
## <a name="configuring-the-web-server-to-use-tcpip-sockets"></a>將 Web 伺服器設定為使用 TCP/IP 通訊端  
 有兩個選項來設定 Web 伺服器，若要使用 TCP/IP Sockets。 您執行的動作取決於是否將所有 SQL Server 都存取從 Web 伺服器，或只有特定的 SQL Server 從 Web 伺服器都存取。  
  
 如果所有 SQL Server 會從 Web 伺服器都存取，您需要在 Web 伺服器電腦上執行 SQL Server 用戶端組態公用程式。 下列步驟變更為從這個 IIS Web 伺服器進行以使用 TCP/IP 通訊端網路程式庫的所有 SQL Server 連線的預設網路程式庫。  
  
### <a name="to-configure-the-web-server-all-sql-servers"></a>若要設定網頁伺服器 (所有 SQL Server)  
  
### <a name="for-microsoft-sql-server-65"></a>Microsoft SQL server 6.5:  
  
1.  從 開始 功能表中，指向 程式、 指向 Microsoft SQL Server 6.5、，然後按一下 SQL 用戶端組態公用程式。  
  
2.  按一下 [網路程式庫] 索引標籤。  
  
3.  在預設的網路] 方塊中，選取 [TCP/IP 通訊端。  
  
4.  按一下 [完成] 以儲存變更並結束此公用程式。  
  
### <a name="for-microsoft-sql-server-70"></a>Microsoft SQL server 7.0:  
  
1.  從 開始 功能表中，指向程式、 指向 Microsoft SQL Server 7.0、，然後按一下 用戶端網路公用程式。  
  
2.  按一下 [一般] 索引標籤。  
  
3.  在 預設的網路程式庫 方塊中，按一下 TCP/IP。  
  
4.  按一下 [確定] 以儲存變更並結束此公用程式。  
  
 從 Web 伺服器存取特定的 SQL Server 時，如果您需要在 Web 伺服器電腦上執行 SQL Server 用戶端組態公用程式。 若要變更為特定的 SQL Server 連線的網路程式庫，請在 Web 伺服器電腦上，如下所示設定 SQL Server 用戶端軟體。  
  
### <a name="to-configure-the-web-server-a-specific-sql-server"></a>若要設定網頁伺服器 (特定 SQL Server)  
  
### <a name="for-microsoft-sql-server-65"></a>Microsoft SQL server 6.5:  
  
1.  從 開始 功能表中，指向 程式、 指向 Microsoft SQL Server 6.5、，然後按一下 SQL 用戶端組態公用程式。  
  
2.  按一下 [進階] 索引標籤。  
  
3.  在 [伺服器] 方塊中，輸入來連接使用 TCP/IP 通訊端伺服器的名稱。  
  
4.  在 DLL 名稱] 方塊中，選取 [TCP/IP 通訊端。  
  
5.  按一下 新增/修改。 指向此伺服器的所有資料來源現在會都使用 TCP/IP 通訊端。  
  
6.  按一下 [完成]。  
  
### <a name="for-microsoft-sql-server-70"></a>Microsoft SQL server 7.0:  
  
1.  從 開始 功能表中，指向程式、 指向 Microsoft SQL Server 7.0、，然後按一下 用戶端組態公用程式。  
  
2.  按一下 [一般] 索引標籤。  
  
3.  按一下 [加入]。  
  
4.  在 [伺服器別名] 方塊中輸入伺服器的別名。 在 網路程式庫 方塊中，按一下 TCP/IP。 在 [電腦名稱] 方塊中，輸入會接聽 TCP/IP 通訊端用戶端電腦的電腦名稱。 在 [連接埠號碼] 方塊中，輸入 SQL Server 所接聽的連接埠。  
  
5.  按一下 [確定]，然後確定要結束此公用程式。  
  
## <a name="see-also"></a>另請參閱  
 [RDS 基本概念](../../../ado/guide/remote-data-service/rds-fundamentals.md)






















