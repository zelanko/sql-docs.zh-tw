---
title: "啟用或停用伺服器網路通訊協定 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "網路通訊協定 [SQL Server], 停用"
  - "遠端連線 [SQL Server], 使用組態管理員啟用"
  - "通訊協定 [SQL Server], 使用組態管理員啟用"
  - "通訊協定 [SQL Server], 使用組態管理員停用"
  - "停用網路通訊協定, 組態管理員"
  - "網路通訊協定 [SQL Server], 啟用"
  - "啟用網路通訊協定, 組態管理員"
  - "介面區組態 [SQL Server], 連線通訊協定"
  - "連線 [SQL Server], 使用組態管理員啟用"
ms.assetid: ec5ccb69-61c9-4576-8843-014b976fd46e
caps.latest.revision: 29
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 29
---
# 啟用或停用伺服器網路通訊協定
  所有網路通訊協定都是由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式所安裝，但是有些會啟用，有些不會啟用。 本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 組態管理員或 PowerShell，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中啟用或停用伺服器網路通訊協定。 必須停止並重新啟動 [!INCLUDE[ssDE](../../includes/ssde-md.md)] ，才能讓變更生效。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 安裝期間會在 BUILTIN\Users 群組中加入一個登入。 這個登入可讓電腦上所有經過驗證的使用者以 public 角色成員的身分存取 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 執行個體。 BUILTIN\Users 登入可以安全地移除，藉此限制擁有個別登入或為其他擁有登入之 Windows 群組成員的電腦使用者對 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的存取。  
  
> [!WARNING]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料提供者支援 TLS 1.0 和 SSL 3.0。 如果您以在作業系統 SChannel 層級中進行變更的方式，強制執行不同的通訊協定 (例如 TLS 1.1 或 TLS 1.2)，您與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的連線可能會失敗。  
  
 **本主題內容**  
  
-   **若要使用下列項目來啟用或停用伺服器網路通訊協定：**  
  
     [SQL Server 組態管理員](#SSMSProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server 組態管理員  
  
#### 若要啟用伺服器網路通訊協定  
  
1.  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員的主控台窗格中，展開 **[SQL Server 網路組態]**。  
  
2.  在主控台窗格中，按一下 [通訊協定] *\<執行個體名稱>*。  
  
3.  在詳細資料窗格中，以滑鼠右鍵按一下要變更的通訊協定，然後按一下 [啟用] 或 [停用]。  
  
4.  在主控台窗格中，按一下 **[SQL Server 服務]**。  
  
5.  在詳細資料窗格中，以滑鼠右鍵按一下 **SQL Server (***\<執行個體名稱>***)**，然後按一下 [重新啟動]，以停止並重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務。  
  
##  <a name="PowerShellProcedure"></a> 使用 SQL Server PowerShell  
  
#### 若要使用 PowerShell 來啟用伺服器網路通訊協定  
  
1.  使用管理員權限來開啟命令提示字元。  
  
2.  從工作列啟動 Windows PowerShell，或是依序按一下 [開始]、[所有程式]、[附屬應用程式]、[Windows PowerShell]，然後按一下 [Windows PowerShell]。  
  
3.  輸入 **Import-Module “sqlps”** 來匯入 **sqlps** 模組  
  
4.  執行下列陳述式，即可同時啟用 TCP 和具名管道通訊協定。 請將 `<computer_name>` 取代成執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的電腦名稱。 如果您要設定具名執行個體，請將 `MSSQLSERVER` 取代成執行個體名稱。  
  
     若要停用通訊協定，請將 `IsEnabled` 屬性設定為 `$false`。  
  
    ```  
    $smo = 'Microsoft.SqlServer.Management.Smo.'  
    $wmi = new-object ($smo + 'Wmi.ManagedComputer').  
  
    # List the object properties, including the instance names.  
    $Wmi  
  
    # Enable the TCP protocol on the default instance.  
    $uri = "ManagedComputer[@Name='<computer_name>']/ ServerInstance[@Name='MSSQLSERVER']/ServerProtocol[@Name='Tcp']"  
    $Tcp = $wmi.GetSmoObject($uri)  
    $Tcp.IsEnabled = $true  
    $Tcp.Alter()  
    $Tcp  
  
    # Enable the named pipes protocol for the default instance.  
    $uri = "ManagedComputer[@Name='<computer_name>']/ ServerInstance[@Name='MSSQLSERVER']/ServerProtocol[@Name='Np']"  
    $Np = $wmi.GetSmoObject($uri)  
    $Np.IsEnabled = $true  
    $Np.Alter()  
    $Np  
    ```  
  
#### 若要設定本機電腦的通訊協定  
  
-   在本機執行此指令碼並且設定本機電腦時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 可能會用動態方式決定本機電腦名稱，讓指令碼更具彈性。 若要擷取本機電腦名稱，請將設定 `$uri` 變數的程式碼行取代成下列程式碼行：  
  
    ```  
    $uri = "ManagedComputer[@Name='" + (get-item env:\computername).Value + "']/ServerInstance[@Name='MSSQLSERVER']/ServerProtocol[@Name='Tcp']"  
    ```  
  
#### 若要使用 SQL Server PowerShell 來重新啟動 Database Engine  
  
-   啟用或停用通訊協定之後，您必須停止並重新啟動 [!INCLUDE[ssDE](../../includes/ssde-md.md)] ，才能讓變更生效。 您可以執行下列陳述式，利用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 來停止並啟用預設執行個體。 若要停止並啟動具名執行個體，請將 `'MSSQLSERVER'` 取代成 `'MSSQL$<instance_name>'`。  
  
    ```  
    # Get a reference to the ManagedComputer class.  
    CD SQLSERVER:\SQL\<computer_name>  
    $Wmi = (get-item .).ManagedComputer  
    # Get a reference to the default instance of the Database Engine.  
    $DfltInstance = $Wmi.Services['MSSQLSERVER']  
    # Display the state of the service.  
    $DfltInstance  
    # Stop the service.  
    $DfltInstance.Stop();  
    # Wait until the service has time to stop.  
    # Refresh the cache.  
    $DfltInstance.Refresh();   
    # Display the state of the service.  
    $DfltInstance  
    # Start the service again.  
    $DfltInstance.Start();  
    # Wait until the service has time to start.  
    # Refresh the cache and display the state of the service.  
    $DfltInstance.Refresh(); $DfltInstance  
    ```  
  
  