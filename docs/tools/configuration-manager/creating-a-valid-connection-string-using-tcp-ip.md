---
title: "建立有效的連接字串使用 TCP IP |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connection strings [Database Engine]
- ports [SQL Server], connecting to
- TCP/IP [SQL Server], connection strings
- connection strings [Database Engine], TCP/IP
- aliases [SQL Server], TCP/IP
ms.assetid: ee5dbc2c-1fc6-42bd-bdf5-efa792557934
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8611848c01d854e373e3e945e9d7c6d69df0c2ce
ms.contentlocale: zh-tw
ms.lasthandoff: 09/28/2017

---
# <a name="creating-a-valid-connection-string-using-tcp-ip"></a>使用 TCP IP 建立有效的連接字串
  若要使用 TCP/IP 建立有效的連接字串，您必須：  
  
-   指定 **別名名稱**。  
  
-   針對 **[伺服器]**，輸入您可以使用 **PING** 公用程式來連接的伺服器名稱，或是可以使用 **PING** 公用程式來連接的 IP 位址。 針對具名執行個體，請附加執行個體名稱。  
  
-   在 **[通訊協定]** 中指定 **[TCP/IP]**。  
  
-   (選擇性) 在 **[通訊埠編號]**中輸入通訊埠編號。 預設值為 1433，也就是伺服器上 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 預設執行個體的通訊埠編號。 若要連接到具名執行個體或未接聽通訊埠 1433 的預設執行個體，您必須提供通訊埠編號，或是啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務。 如需設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務的資訊，請參閱 [SQL Server Browser 服務](../../tools/configuration-manager/sql-server-browser-service.md)。  
  
 在連接時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 元件會從登錄中讀取指定之別名名稱的伺服器、通訊協定與通訊埠值，並以 `tcp:<servername>[\<instancename>],<port>` 或 `tcp:<IPAddress>[\<instancename>],<port>`格式建立連接字串。  
  
> [!NOTE]  
>  根據預設， [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 防火牆會關閉通訊埠 1433。 由於 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是透過連接埠 1433 來進行通訊，因此如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 設定為使用 TCP/IP 來接聽內送的用戶端連接，您就必須重新開啟該通訊埠。 如需設定防火牆的相關資訊，請參閱《 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜如何：設定防火牆供 SQL Server 存取＞，或請檢閱您的防火牆文件集。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 完整支援 Internet Protocol 第 4 版 (IPv4) 和 Internet Protocol 第 6 版 (IPv6)。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員可以接受 IPv4 和 IPv6 格式的 IP 位址。 如需有關 IPv6 的資訊，請參閱《 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜使用 IPv6 連接＞。  
  
## <a name="connecting-to-the-local-server"></a>連接到本機伺服器  
 連接到與用戶端在同一部電腦上執行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，可以使用 `(local)` 做為伺服器名稱。 但不建議這麼做，因為會造成模糊不清，但是若確實知道用戶端正在預期的電腦上執行，這就很有用。 例如，為行動式、非連接的使用者 (例如銷售人員) 建立應用程式 (亦即 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將會在膝上型電腦上執行並儲存專案資料) 時，連接到 `(local)` 的用戶端一律會連接到在膝上型電腦上執行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 可以使用字詞 `localhost` 或句點 (**.**) 來取代 `(local)`。  
  
## <a name="verifying-your-connection-protocol"></a>驗證您的連接通訊協定  
 下列查詢會傳回目前連接所使用的通訊協定。  
  
```  
SELECT net_transport   
FROM sys.dm_exec_connections   
WHERE session_id = @@SPID;  
  
```  
  
## <a name="examples"></a>範例  
 使用伺服器名稱連接：  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             <servername>  
  
```  
  
 使用伺服器名稱連接到具名執行個體：  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             <servername>\<instancename>  
  
```  
  
 使用伺服器名稱來連接指定的通訊埠：  
  
```  
Alias Name         <serveralias>  
Port No            <port>  
Protocol           TCP/IP  
Server             <servername>  
  
```  
  
 使用 IP 位址來連接：  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             <IPAddress>  
  
```  
  
 使用 IP 位址連接到具名執行個體：  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             <IPAddress>\<instancename>  
  
```  
  
 使用 IP 位址連接到指定的通訊埠：  
  
```  
Alias Name         <serveralias>  
Port No            <port number>  
Protocol           TCP/IP  
Server             <IPAddress>  
  
```  
  
 使用 `(local)`連接到本機電腦：  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             (local)  
  
```  
  
 使用 `localhost`連接到本機電腦：  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             localhost  
  
```  
  
 連接到本機電腦 `localhost`上的具名執行個體：  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             localhost\<instancename>  
  
```  
  
 使用句點連接到本機電腦：  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             .  
  
```  
  
 使用句點連接到本機電腦上的具名執行個體：  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             .\<instancename>  
  
```  
  
> [!NOTE]  
>  如需指定網路通訊協定作為 **sqlcmd** 參數的資訊，請參閱《 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜如何：使用 sqlcmd.exe 連接到 Database Engine＞。  
  
## <a name="see-also"></a>另請參閱  
 [使用共用記憶體通訊協定建立有效的連接字串](../../tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)   
 [建立有效的連接字串使用具名的管道](http://msdn.microsoft.com/library/90930ff2-143b-4651-8ae3-297103600e4f)   
 [選擇網路通訊協定](http://msdn.microsoft.com/library/6565fb7d-b076-4447-be90-e10d0dec359a)  
  
  
