---
title: 搭配 ODBC 連接共用使用 RDS |Microsoft Docs
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
ms.openlocfilehash: a2ffcc64cb9d0e45d371e927cd1c15be51cd917c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67921930"
---
# <a name="using-rds-with-odbc-connection-pooling"></a>搭配 ODBC 連線集區使用 RDS
如果您使用的是 ODBC 資料來源，您可以使用 Internet Information Services （IIS）中的 [連接共用] 選項，以達成用戶端負載的高效能處理。 連接共用是連接的資源管理員，可維護常用連線的開啟狀態。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 若要啟用連接共用，請參閱 Internet Information Services 檔。  
  
 請注意，啟用連線共用可能會使網頁伺服器受限於其他限制，如 Microsoft Internet Information Services 檔中所述。  
  
 若要確保連線共用穩定，並提供額外的效能提升，您必須將 Microsoft SQL Server 設定為使用 TCP/IP 通訊端網路程式庫。  
  
 若要這樣做，您需要：  
  
-   將 SQL Server 電腦設定為使用 TCP/IP 通訊端。  
  
-   將網頁伺服器設定為使用 TCP/IP 通訊端。  
  
## <a name="configuring-the-sql-server-computer-to-use-tcpip-sockets"></a>將 SQL Server 電腦設定為使用 TCP/IP 通訊端  
 在 SQL Server 電腦上，執行 SQL Server 安裝程式，讓與資料來源的互動使用 TCP/IP 通訊端網路程式庫。  
  
### <a name="to-specify-the-tcpip-socket-network-library-on-the-sql-server-computer"></a>若要指定 SQL Server 電腦上的 TCP/IP 通訊端網路程式庫  
  
### <a name="in-microsoft-sql-server-65"></a>在 Microsoft SQL Server 6.5：  
  
1.  在 [開始] 功能表中，依序指向 [程式] 和 [Microsoft SQL Server 6.5]，然後按一下 [SQL 安裝程式]。  
  
2.  按兩次 [繼續]。  
  
3.  在 [Microsoft SQL Server 選項] 對話方塊中，選取 [變更網路支援]，然後按一下 [繼續]。  
  
4.  請確定已選取 [TCP/IP 通訊端] 核取方塊，然後按一下 [確定]。  
  
5.  按一下 [繼續] 完成，並結束安裝程式。  
  
### <a name="in-microsoft-sql-server-70"></a>在 Microsoft SQL Server 7.0：  
  
1.  在 [開始] 功能表中，依序指向 [程式]、[Microsoft SQL Server 7.0]，然後按一下 [伺服器網路公用程式]。  
  
2.  在對話方塊的 [一般] 索引標籤上，按一下 [新增]。  
  
3.  在 [新增網路程式庫設定] 對話方塊中，按一下 [TCP/IP]。  
  
4.  在 [埠號碼] 和 [Proxy 位址] 方塊中，輸入您的網路系統管理員所提供的埠號碼和 proxy 位址。  
  
5.  按一下 [確定] 以完成，並結束安裝程式。  
  
## <a name="configuring-the-web-server-to-use-tcpip-sockets"></a>設定網頁伺服器使用 TCP/IP 通訊端  
 有兩個選項可將 Web 服務器設定為使用 TCP/IP 通訊端。 您所執行的動作取決於是否從 Web 服務器存取所有 SQL Server，或只從 Web 服務器存取特定的 SQL Server。  
  
 如果從 Web 服務器存取所有 SQL server，您必須在 Web 服務器電腦上執行 SQL Server 用戶端設定公用程式。 下列步驟會變更從這個 IIS Web 服務器進行的所有 SQL Server 連線的預設網路程式庫，以使用 TCP/IP 通訊端網路程式庫。  
  
### <a name="to-configure-the-web-server-all-sql-servers"></a>設定網頁伺服器（所有 SQL server）  
  
### <a name="for-microsoft-sql-server-65"></a>針對 Microsoft SQL Server 6.5：  
  
1.  在 [開始] 功能表中，依序指向 [程式]、[Microsoft SQL Server 6.5]，然後按一下 [SQL Client 設定公用程式]。  
  
2.  按一下 [網路程式庫] 索引標籤。  
  
3.  在 [預設網路] 方塊中，選取 [TCP/IP 通訊端]。  
  
4.  按一下 [完成] 以儲存變更並結束公用程式。  
  
### <a name="for-microsoft-sql-server-70"></a>針對 Microsoft SQL Server 7.0：  
  
1.  在 [開始] 功能表中，依序指向 [程式]、[Microsoft SQL Server 7.0]，然後按一下 [用戶端網路公用程式]。  
  
2.  按一下 [一般] 索引標籤。  
  
3.  在 [預設網路程式庫] 方塊中，按一下 [TCP/IP]。  
  
4.  按一下 [確定] 以儲存變更並結束公用程式。  
  
 如果從 Web 服務器存取特定的 SQL Server，您必須在 Web 服務器電腦上執行 SQL Server 用戶端設定公用程式。 若要變更特定 SQL Server 連線的網路程式庫，請在 Web 服務器電腦上設定 SQL Server 用戶端軟體，如下所示。  
  
### <a name="to-configure-the-web-server-a-specific-sql-server"></a>設定網頁伺服器（特定 SQL Server）  
  
### <a name="for-microsoft-sql-server-65"></a>針對 Microsoft SQL Server 6.5：  
  
1.  在 [開始] 功能表中，依序指向 [程式]、[Microsoft SQL Server 6.5]，然後按一下 [SQL Client 設定公用程式]。  
  
2.  按一下 [進階] 索引標籤。  
  
3.  在 [伺服器] 方塊中，輸入使用 TCP/IP 通訊端連接的伺服器名稱。  
  
4.  在 [DLL 名稱] 方塊中，選取 [TCP/IP 通訊端]。  
  
5.  按一下 [新增/修改]。 所有指向這部伺服器的資料來源現在都會使用 TCP/IP 通訊端。  
  
6.  按一下 [完成]。  
  
### <a name="for-microsoft-sql-server-70"></a>針對 Microsoft SQL Server 7.0：  
  
1.  在 [開始] 功能表中，依序指向 [程式]、[Microsoft SQL Server 7.0]，然後按一下 [用戶端設定公用程式]。  
  
2.  按一下 [一般] 索引標籤。  
  
3.  按一下 [加入]。  
  
4.  在 [伺服器別名] 方塊中輸入伺服器的別名。 在 [網路程式庫] 方塊中，按一下 [TCP/IP]。 在 [電腦名稱稱] 方塊中，輸入接聽 TCP/IP 通訊端用戶端之電腦的電腦名稱稱。 在 [埠號碼] 方塊中，輸入 SQL Server 接聽的埠。  
  
5.  按一下 [確定]，然後再按一次 [確定] 以結束公用程式。  
  
## <a name="see-also"></a>另請參閱  
 [RDS 基本概念](../../../ado/guide/remote-data-service/rds-fundamentals.md)






















