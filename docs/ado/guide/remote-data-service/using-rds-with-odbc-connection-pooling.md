---
description: 搭配 ODBC 連線集區使用 RDS
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 440a1947d5424840ec99f9e4da7ae03266c7ac04
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88451860"
---
# <a name="using-rds-with-odbc-connection-pooling"></a>搭配 ODBC 連線集區使用 RDS
如果您使用的是 ODBC 資料來源，您可以使用 Internet Information Services (IIS) 中的 [連接共用] 選項，以達到用戶端負載的高效能處理。 連接共用是連接的資源管理員，可維護常用連接的開啟狀態。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 若要啟用連接共用，請參閱 Internet Information Services 檔。  
  
 請注意，啟用連線共用可能會導致 Web 服務器遭受其他限制，如 Microsoft Internet Information Services 檔中所述。  
  
 若要確保連接共用穩定，並提供額外的效能提升，您必須將 Microsoft SQL Server 設定為使用 TCP/IP 通訊端網路程式庫。  
  
 若要這樣做，您需要：  
  
-   將 SQL Server 電腦設定為使用 TCP/IP 通訊端。  
  
-   將網頁伺服器設定為使用 TCP/IP 通訊端。  
  
## <a name="configuring-the-sql-server-computer-to-use-tcpip-sockets"></a>設定 SQL Server 電腦使用 TCP/IP 通訊端  
 在 SQL Server 電腦上執行 SQL Server 安裝程式，以便與資料來源的互動使用 TCP/IP 通訊端網路程式庫。  
  
### <a name="to-specify-the-tcpip-socket-network-library-on-the-sql-server-computer"></a>在 SQL Server 電腦上指定 TCP/IP 通訊端網路程式庫  
  
### <a name="in-microsoft-sql-server-65"></a>在 Microsoft SQL Server 6.5：  
  
1.  在 [[開始] 功能表] 中，依序指向 [程式] 和 [Microsoft SQL Server 6.5]，然後按一下 [SQL 安裝程式]。  
  
2.  按兩次 [繼續]。  
  
3.  在 [Microsoft SQL Server 選項] 對話方塊中，選取 [變更網路支援]，然後按一下 [繼續]。  
  
4.  確認 [TCP/IP 通訊端] 核取方塊已選取，然後按一下 [確定]。  
  
5.  按一下 [繼續] 以完成，然後結束安裝程式。  
  
### <a name="in-microsoft-sql-server-70"></a>在 Microsoft SQL Server 7.0：  
  
1.  在 [[開始] 功能表] 中，依序指向 [程式] 和 [Microsoft SQL Server 7.0]，然後按一下 [伺服器網路公用程式]。  
  
2.  在對話方塊的 [一般] 索引標籤上，按一下 [新增]。  
  
3.  在 [新增網路程式庫設定] 對話方塊中，按一下 [TCP/IP]。  
  
4.  在 [埠號碼] 和 [Proxy 位址] 方塊中，輸入網路系統管理員所提供的埠號碼和 proxy 位址。  
  
5.  按一下 [確定] 完成，然後結束安裝程式。  
  
## <a name="configuring-the-web-server-to-use-tcpip-sockets"></a>設定 Web 服務器使用 TCP/IP 通訊端  
 有兩個選項可用來設定 Web 服務器使用 TCP/IP 通訊端。 您所做的動作取決於是否從 Web 服務器存取所有的 SQL server，或只從 Web 服務器存取特定的 SQL Server。  
  
 如果從 Web 服務器存取所有的 SQL server，您必須在 Web 服務器電腦上執行 SQL Server 用戶端設定公用程式。 下列步驟會變更從此 IIS Web 服務器進行的所有 SQL Server 連接的預設網路程式庫，以使用 TCP/IP 通訊端網路程式庫。  
  
### <a name="to-configure-the-web-server-all-sql-servers"></a>若要設定 Web 服務器 (所有的 SQL server)   
  
### <a name="for-microsoft-sql-server-65"></a>針對 Microsoft SQL Server 6.5：  
  
1.  在 [[開始] 功能表] 中，依序指向 [程式] 和 [Microsoft SQL Server 6.5]，然後按一下 [SQL 用戶端設定公用程式]。  
  
2.  按一下 [網路程式庫] 索引標籤。  
  
3.  在 [預設網路] 方塊中，選取 [TCP/IP 通訊端]。  
  
4.  按一下 [完成] 以儲存變更並結束公用程式。  
  
### <a name="for-microsoft-sql-server-70"></a>針對 Microsoft SQL Server 7.0：  
  
1.  在 [[開始] 功能表] 中，依序指向 [程式] 和 [Microsoft SQL Server 7.0]，然後按一下 [用戶端網路公用程式]。  
  
2.  按一下 [一般] 索引標籤。  
  
3.  在 [預設網路程式庫] 方塊中，按一下 [TCP/IP]。  
  
4.  按一下 [確定] 以儲存變更並結束公用程式。  
  
 如果從 Web 服務器存取特定的 SQL Server，您必須在 Web 服務器電腦上執行 SQL Server 用戶端設定公用程式。 若要變更特定 SQL Server 連線的網路程式庫，請在 Web 服務器電腦上設定 SQL Server 用戶端軟體，如下所示。  
  
### <a name="to-configure-the-web-server-a-specific-sql-server"></a>若要設定 Web 服務器 (特定的 SQL Server)   
  
### <a name="for-microsoft-sql-server-65"></a>針對 Microsoft SQL Server 6.5：  
  
1.  在 [[開始] 功能表] 中，依序指向 [程式] 和 [Microsoft SQL Server 6.5]，然後按一下 [SQL 用戶端設定公用程式]。  
  
2.  按一下 [進階] 索引標籤。  
  
3.  在 [伺服器] 方塊中，輸入要使用 TCP/IP 通訊端連接的伺服器名稱。  
  
4.  在 [DLL 名稱] 方塊中，選取 [TCP/IP 通訊端]。  
  
5.  按一下 [新增/修改]。 所有指向此伺服器的資料來源現在都會使用 TCP/IP 通訊端。  
  
6.  按一下 [完成]。  
  
### <a name="for-microsoft-sql-server-70"></a>針對 Microsoft SQL Server 7.0：  
  
1.  在 [[開始] 功能表] 中，依序指向 [程式] 和 [Microsoft SQL Server 7.0]，然後按一下 [用戶端設定公用程式]。  
  
2.  按一下 [一般] 索引標籤。  
  
3.  按一下 [加入]。  
  
4.  在 [伺服器別名] 方塊中輸入伺服器的別名。 在 [網路程式庫] 方塊中，按一下 [TCP/IP]。 在 [電腦名稱稱] 方塊中，輸入接聽 TCP/IP 通訊端用戶端之電腦的電腦名稱稱。 在 [埠號碼] 方塊中，輸入 SQL Server 接聽的埠。  
  
5.  按一下 [確定]，然後再按一下 [確定] 以結束公用程式。  
  
## <a name="see-also"></a>另請參閱  
 [RDS 基本概念](../../../ado/guide/remote-data-service/rds-fundamentals.md)






















