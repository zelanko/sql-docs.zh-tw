---
title: "伺服器網路組態 | Microsoft Docs"
ms.custom: 
ms.date: 07/27/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Named Pipes [SQL Server], configuring
- connections [SQL Server], server network configuration
- Database Engine [SQL Server], network configurations
- server network configuration [SQL Server]
- protocols [SQL Server], choosing
- ports [SQL Server], changing
- server configuration [SQL Server]
ms.assetid: 890c09a1-6dad-4931-aceb-901c02ae34c5
caps.latest.revision: 50
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 45fe0d96d38f91d8515422380f06a0a661cce0c4
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="server-network-configuration"></a>伺服器網路組態
  伺服器網路組態工作包括啟用通訊協定、修改通訊協定使用的通訊埠或管道、設定加密選項、設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務、在網路上公開或隱藏 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 以及註冊伺服器主體名稱。 大部分的情況下，您不需要變更伺服器網路組態。 除非有特殊的網路需求時，才需要重新設定伺服器網路通訊協定。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的網路組態是利用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員進行設定。 如果是舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，請使用這些產品隨附的伺服器網路公用程式。  
  
## <a name="protocols"></a>通訊協定  
 請利用「 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員」來啟用或停用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]所使用的通訊協定，並設定通訊協定可用的選項。 可啟用一個以上的通訊協定。 您必須啟用要給用戶端使用的所有通訊協定。 所有通訊協定對伺服器的存取權限全部相同。 如需應該使用哪些通訊協定的資訊，請參閱 [啟用或停用伺服器網路通訊協定](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md) 及 [Default SQL Server Network Protocol Configuration](../../database-engine/configure-windows/default-sql-server-network-protocol-configuration.md)(預設 SQL Server 網路通訊協定設定)。  
  
### <a name="changing-a-port"></a>變更通訊埠  
 您可以設定 TCP/IP 通訊協定來接聽指定的通訊埠。 根據預設， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的預設執行個體會接聽 TCP 通訊埠 1433。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 和 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 的具名執行個體是針對動態通訊埠所設定。 這表示，當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務啟動時，它們會選取可用的通訊埠。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務可協助用戶端識別所連接的通訊埠。  
  
 設定為動態通訊埠時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 每次啟動時可能會變更所使用的通訊埠。 透過防火牆連接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，您必須開啟 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]所使用的通訊埠。 請設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用特定的通訊埠，讓您可以設定防火牆來允許對伺服器的通訊。 如需詳細資訊，請參閱[設定伺服器接聽特定 TCP 通訊埠 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md)。  
  
### <a name="changing-a-named-pipe"></a>變更具名管道  
 您可以設定具名管道通訊協定來接聽指定的具名管道。 依預設，[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的預設執行個體會接聽管道 \\\\.\pipe\sql\query (對於預設執行個體) 和 \\\\.\pipe\MSSQL$*\<執行個體名稱>*\sql\query (對於具名執行個體)。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 只能接聽一個具名管道，但您可以視需要將該管道變更為其他名稱。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務可協助用戶端識別所連接的管道。 如需詳細資訊，請參閱[設定接聽替代管道的伺服器 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/configure-a-server-to-listen-on-an-alternate-pipe.md)。  
  
## <a name="force-encryption"></a>強制加密  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 可以設定為和用戶端應用程式通訊時需要加密。 如需詳細資訊，請參閱[啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
## <a name="extended-protection-for-authentication"></a>驗證擴充保護  
 使用繫結和服務繫結的驗證擴充保護可供支援擴充保護的作業系統使用。 如需詳細資訊，請參閱 [使用擴充保護連接至 Database Engine](../../database-engine/configure-windows/connect-to-the-database-engine-using-extended-protection.md)。  
  
## <a name="authenticating-by-using-kerberos"></a>使用 Kerberos 驗證  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援 Kerberos 驗證。 如需詳細資訊，請參閱 [註冊 Kerberos 連接的服務主體名稱](../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md) 和 [Microsoft Kerberos Configuration Manager for SQL Server](http://www.microsoft.com/download/details.aspx?id=39046)。  
  
### <a name="registering-a-server-principal-name-spn"></a>註冊伺服器主體名稱 (SPN)  
 Kerberos 驗證服務會使用 SPN 來驗證服務。 如需詳細資訊，請參閱 [註冊 Kerberos 連接的服務主體名稱](../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)。  
  
 SPN 在使用 NTLM 連接時，可能也會用來讓用戶端驗證變得更安全。 如需詳細資訊，請參閱 [使用擴充保護連接至 Database Engine](../../database-engine/configure-windows/connect-to-the-database-engine-using-extended-protection.md)。  
  
## <a name="sql-server-browser-service"></a>SQL Server Browser 服務  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務會在伺服器上執行，並協助用戶端電腦尋找 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務不需設定，但它在某些連接狀況時必須是執行狀態。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 的詳細資訊，請參閱 [SQL Server Browser 服務 &#40;Database Engine 和 SSAS&#41;](../../database-engine/configure-windows/sql-server-browser-service-database-engine-and-ssas.md)  
  
## <a name="hiding-sql-server"></a>隱藏 SQL Server  
 執行時 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 會以每個已安裝執行個體的名稱、版本與連接資訊來回應查詢。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中， **HideInstance** 旗標表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 不應回應關於此伺服器執行個體的資訊。 用戶端應用程式仍然可以連接，但必須知道必要的連接資訊。 如需詳細資訊，請參閱 [隱藏 SQL Server Database Engine 的執行個體](../../database-engine/configure-windows/hide-an-instance-of-sql-server-database-engine.md)。  
  
## <a name="related-content"></a>相關內容  
 [用戶端網路組態](../../database-engine/configure-windows/client-network-configuration.md)  
  
 [管理 Database Engine Services](../../database-engine/configure-windows/manage-the-database-engine-services.md)  
  
  

