---
title: 使用具名管道建立有效的連接字串 |Microsoft Docs
description: 瞭解如何在使用具名管道通訊協定連接到 SQL Server 的實例時，建立有效的連接字串。 查看有效管道名稱的範例。
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- connection strings [Database Engine], named pipes
- pipes [SQL Server]
- pipes [SQL Server], connecting to
- aliases [SQL Server], named pipes
- Named Pipes [SQL Server], connection strings
ms.assetid: 90930ff2-143b-4651-8ae3-297103600e4f
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 65fcebc3bbe12061e699106fb23eed15a5498414
ms.sourcegitcommit: c8e45e0fdab8ea2ae1c7e709346354576b18ca1e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2020
ms.locfileid: "84716705"
---
# <a name="creating-a-valid-connection-string-using-named-pipes"></a>使用具名管道建立有效的連接字串
  除非使用者變更，否則當的預設實例 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接聽具名管道通訊協定時，它會使用 `\\.\pipe\sql\query` 做為管道名稱。 其中句點表示該電腦為本機電腦， `pipe` 表示連接是具名管道，而 `sql\query` 則是管道的名稱。 若要連接到預設管道，別名必須用 `\\<computer_name>\pipe\sql\query` 做為管道名稱。 若將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 設定為接聽其他管道，則管道名稱必須使用該管道。 例如，如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以 `\\.\pipe\unit\app` 做為管道，則別名必須以 `\\<computer_name>\pipe\unit\app` 做為管道名稱。  
  
 若要建立有效的管道名稱，您必須：  
  
-   指定 **別名名稱**。  
  
-   選取 **[具名管道]** 做為 **[通訊協定]**。  
  
-   輸入 **[管道名稱]**。 或者，您可以將 **[管道名稱]** 留白，在您指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [通訊協定] **與** [伺服器] **之後，** 組態管理員便會完成適當的管道名稱。  
  
-   指定 **[伺服器]**。 對於具名執行個體，您可以提供伺服器名稱與執行個體名稱。  
  
 在連接時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 元件會從登錄中讀取指定之別名名稱的伺服器、通訊協定和管道名稱值，並以或格式建立管道名稱 `np:\\<computer_name>\pipe\<pipename>` `np:\\<IPAddress>\pipe\<pipename>` 。若為已命名的實例，預設的管道名稱是 `\\<computer_name>\pipe\MSSQL$<instance_name>\sql\query` 。  
  
> [!NOTE]  
>  根據預設， [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 防火牆會關閉通訊埠 445。 由於 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是透過通訊埠 445 來進行通訊，因此如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 設定為使用具名管道來接聽內送的用戶端連接，您就必須重新開啟該連接埠。 如需設定防火牆的相關資訊，請參閱《 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜如何：設定防火牆供 SQL Server 存取＞，或請檢閱您的防火牆文件集。  
  
## <a name="connecting-to-the-local-server"></a>連接到本機伺服器  
 連接到與用戶端在同一部電腦上執行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，可以使用 `(local)`做為伺服器名稱。 但不建議您使用 `(local)` ，因為這會造成混淆，但是若確實知道用戶端正在預期的電腦上執行，這就很有用。 例如，為行動式、非連接的使用者 (例如銷售人員) 建立應用程式 (亦即 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將會在膝上型電腦上執行並儲存專案資料) 時，連接到 (local) 的用戶端一律會連接到在膝上型電腦上執行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 可以使用 `localhost` 或句點 (.) 來取代 `(local)`。  
  
## <a name="verifying-your-connection-protocol"></a>驗證您的連接通訊協定  
 下列查詢會傳回目前連接所使用的通訊協定。  
  
```  
SELECT net_transport   
FROM sys.dm_exec_connections   
WHERE session_id = @@SPID;  
  
```  
  
## <a name="examples"></a>範例  
 使用伺服器名稱連接到預設管道：  
  
```  
Alias Name         <serveralias>  
Pipe Name          <blank>  
Protocol           Named Pipes  
Server             <servername>  
  
```  
  
 使用 IP 位址連接到預設管道：  
  
```  
Alias Name         <serveralias>  
Pipe Name          <leave blank>  
Protocol           Named Pipes  
Server             <IPAddress>  
  
```  
  
 使用伺服器名稱連接到非預設管道：  
  
```  
Alias Name         <serveralias>  
Pipe Name          \\<servername>\pipe\unit\app  
Protocol           Named Pipes  
Server             <servername>  
  
```  
  
 使用伺服器名稱連接到具名執行個體：  
  
```  
Alias Name         <serveralias>  
Pipe Name          \\<servername>\pipe\MSSQL$<instancename>\SQL\query  
Protocol           Named Pipes  
Server             <servername>  
  
```  
  
 使用 `localhost`連接到本機電腦：  
  
```  
Alias Name         <serveralias>  
Pipe Name          <blank>  
Protocol           Named Pipes  
Server             localhost  
  
```  
  
 使用句點連接到本機電腦：  
  
```  
Alias Name         <serveralias>  
Pipe Name          <left blank>  
Protocol           Named Pipes  
Server             .  
  
```  
  
> [!NOTE]  
>  若要指定網路通訊協定做為 **sqlcmd** 參數，請參閱「如何：《 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜如何：使用 sqlcmd.exe 連接至 Database Engine＞。  
  
## <a name="see-also"></a>另請參閱  
 [使用共用記憶體通訊協定建立有效的連接字串](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)   
 [使用 TCP IP 建立有效的連接字串](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)   
 [選擇網路通訊協定](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)  
  
  
