---
title: 設定 SMO 中的 SQL Server |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server, configuring
- configuration options [SMO]
ms.assetid: 0a372643-15cb-45a7-8665-04f1215df8ed
author: stevestein
ms.author: sstein
ms.openlocfilehash: a05a318f0db624c2423d43759d4b47913179574b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "84996984"
---
# <a name="configuring-sql-server-in-smo"></a>在 SMO 中設定 SQL Server
  在 SMO 中，物件 <xref:Microsoft.SqlServer.Management.Smo.Information> 、 <xref:Microsoft.SqlServer.Management.Smo.Settings> 物件、物件 <xref:Microsoft.SqlServer.Management.Smo.UserOptions> 和物件都 <xref:Microsoft.SqlServer.Management.Smo.Configuration> 包含實例的設定和資訊 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 具有多個描述已安裝之執行個體行為的屬性。 這些屬性描述啟動選項、伺服器預設值、檔案和目錄、系統和處理資訊、產品和版本、連接資訊、記憶體選項、語言和定序選取項目，以及驗證模式。  
  
## <a name="sql-server-configuration"></a>SQL Server 組態  
 <xref:Microsoft.SqlServer.Management.Smo.Information> 物件屬性包含有關 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體 (例如處理器和平台) 的詳細資訊。  
  
 <xref:Microsoft.SqlServer.Management.Smo.Settings> 物件屬性包含有關 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的詳細資訊。 除了郵件設定檔和伺服器帳戶外，您也可以修改預設的資料庫檔案和目錄。 在連接持續時間會保留這些屬性。  
  
 <xref:Microsoft.SqlServer.Management.Smo.UserOptions> 物件屬性包含目前與算術、ANSI 標準和交易相關之連接行為的詳細資訊。  
  
 此外也有一組由 <xref:Microsoft.SqlServer.Management.Smo.Configuration> 物件所代表的組態選項。 其中包含一組屬性，代表可由 `sp_configure` 預存程序修改的選項。 [**優先權提升**]、[復原**間隔**] 和 [**網路封包大小**] 等選項會控制實例的效能 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。 這其中許多選項都可以動態變更，但在某些情況下，當 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的執行個體重新啟動時，會先設定值然後再加以變更。  
  
 每個組態選項都有 <xref:Microsoft.SqlServer.Management.Smo.Configuration> 物件屬性。 您可以使用 <xref:Microsoft.SqlServer.Management.Smo.ConfigProperty> 物件來修改全域組態設定。 許多屬性都擁有最大和最小值，這些值也會儲存為 <xref:Microsoft.SqlServer.Management.Smo.ConfigProperty> 屬性。 這些屬性需要 <xref:Microsoft.SqlServer.Management.Smo.ConfigurationBase.Alter%2A> 方法才能認可對實例的變更 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
 <xref:Microsoft.SqlServer.Management.Smo.Configuration> 物件中的所有組態選項都必須由系統管理員變更。  
  
## <a name="examples"></a>範例  
 在下列的程式碼範例中，您必須選取用於建立應用程式的程式設計環境、程式設計範本和程式設計語言。 如需詳細資訊，請參閱[在 Visual Studio .net 中建立 VISUAL BASIC SMO 專案](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md)和[在 Visual Studio .Net 中建立 VISUAL C&#35; SMO 專案](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
  
## <a name="modifying-sql-server-configuration-options-in-visual-basic"></a>在 Visual Basic 中修改 SQL Server 組態選項  
 此程式碼範例會顯示如何在 Visual Basic .NET 中更新組態選項， 也會擷取並顯示有關指定組態選項最大及最小值的詳細資訊。 最後，此程式會通知使用者變更是否是以動態方式進行，或者在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的執行個體重新啟動之前都會儲存變更。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBConfigure2](SMO How to#SMO_VBConfigure2)]  -->  
  
## <a name="modifying-sql-server-settings-in-visual-basic"></a>在 Visual Basic 中修改 SQL Server 設定  
 此程式碼範例會在和中顯示實例的相關資訊 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] <xref:Microsoft.SqlServer.Management.Smo.Information> <xref:Microsoft.SqlServer.Management.Smo.Settings> ，並修改 <xref:Microsoft.SqlServer.Management.Smo.Settings> 和 <xref:Microsoft.SqlServer.Management.Smo.UserOptions> 物件屬性中的設定。  
  
 在此範例中，<xref:Microsoft.SqlServer.Management.Smo.UserOptions> 物件和 <xref:Microsoft.SqlServer.Management.Smo.Settings> 物件兩者都擁有 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A> 方法。 您可以個別地為這些執行 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A> 方法。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBConfigure1](SMO How to#SMO_VBConfigure1)]  -->  
  
## <a name="modifying-sql-server-settings-in-visual-c"></a>在 Visual C# 中修改 SQL Server 設定  
 此程式碼範例會在和中顯示實例的相關資訊 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] <xref:Microsoft.SqlServer.Management.Smo.Information> <xref:Microsoft.SqlServer.Management.Smo.Settings> ，並修改 <xref:Microsoft.SqlServer.Management.Smo.Settings> 和 <xref:Microsoft.SqlServer.Management.Smo.UserOptions> 物件屬性中的設定。  
  
 在此範例中，<xref:Microsoft.SqlServer.Management.Smo.UserOptions> 物件和 <xref:Microsoft.SqlServer.Management.Smo.Settings> 物件兩者都擁有 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A> 方法。 您可以個別地為這些執行 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A> 方法。  
  
 `//Connect to the local, default instance of SQL Server.`  
  
```csharp
{  
            Server srv = new Server();  
            //Display all the configuration options.   
  
            foreach (ConfigProperty p in srv.Configuration.Properties)  
            {  
                Console.WriteLine(p.DisplayName);  
            }  
            Console.WriteLine("There are " + srv.Configuration.Properties.Count.ToString() + " configuration options.");  
            //Display the maximum and minimum values for ShowAdvancedOptions.   
            int min = 0;  
            int max = 0;  
            min = srv.Configuration.ShowAdvancedOptions.Minimum;  
            max = srv.Configuration.ShowAdvancedOptions.Maximum;  
            Console.WriteLine("Minimum and Maximum values are " + min + " and " + max + ".");  
            //Modify the value of ShowAdvancedOptions and run the Alter method.   
            srv.Configuration.ShowAdvancedOptions.ConfigValue = 0;  
            srv.Configuration.Alter();  
            //Display when the change takes place according to the IsDynamic property.   
            if (srv.Configuration.ShowAdvancedOptions.IsDynamic == true)  
            {  
                Console.WriteLine("Configuration option has been updated.");  
            }  
            else  
            {  
                Console.WriteLine("Configuration option will be updated when SQL Server is restarted.");  
            }  
        }  
```  
  
## <a name="modifying-sql-server-settings-in-powershell"></a>在 PowerShell 中修改 SQL Server 設定  
 此程式碼範例會在和中顯示實例的相關資訊 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] <xref:Microsoft.SqlServer.Management.Smo.Information> <xref:Microsoft.SqlServer.Management.Smo.Settings> ，並修改 <xref:Microsoft.SqlServer.Management.Smo.Settings> 和 <xref:Microsoft.SqlServer.Management.Smo.UserOptions> 物件屬性中的設定。  
  
 在此範例中，<xref:Microsoft.SqlServer.Management.Smo.UserOptions> 物件和 <xref:Microsoft.SqlServer.Management.Smo.Settings> 物件兩者都擁有 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A> 方法。 您可以個別地為這些執行 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A> 方法。  
  
```powershell
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\  
$srv = Get-Item default  
  
#Display information about the instance of SQL Server in Information and Settings.  
"OS Version = " + $srv.Information.OSVersion  
"State = "+ $srv.Settings.State.ToString()  
  
#Display information specific to the current user in UserOptions.  
"Quoted Identifier support = " + $srv.UserOptions.QuotedIdentifier  
  
#Modify server settings in Settings.  
$srv.Settings.LoginMode = [Microsoft.SqlServer.Management.SMO.ServerLoginMode]::Integrated  
  
#Modify settings specific to the current connection in UserOptions.  
$srv.UserOptions.AbortOnArithmeticErrors = $true  
  
#Run the Alter method to make the changes on the instance of SQL Server.  
$srv.Alter()  
```  
  
## <a name="modifying-sql-server-configuration-options-in-powershell"></a>在 PowerShell 中修改 SQL Server 組態選項  
 此程式碼範例會顯示如何在 Visual Basic .NET 中更新組態選項， 也會擷取並顯示有關指定組態選項最大及最小值的詳細資訊。 最後，此程式會通知使用者變更是否是以動態方式進行，或者在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的執行個體重新啟動之前都會儲存變更。  
  
```powershell
#Get a server object which corresponds to the default instance replace LocalMachine with the physical server  
cd \sql\LocalMachine  
$svr = Get-Item default  
  
#enumerate its properties  
foreach ($Item in $Svr.Configuration.Properties)   
{  
 $Item.DisplayName  
}  
  
"There are " + $svr.Configuration.Properties.Count.ToString() + " configuration options."  
  
#Display the maximum and minimum values for ShowAdvancedOptions.  
$min = $svr.Configuration.ShowAdvancedOptions.Minimum  
$max = $svr.Configuration.ShowAdvancedOptions.Maximum  
"Minimum and Maximum values are " + $min.ToString() + " and " + $max.ToString() + "."  
  
#Modify the value of ShowAdvancedOptions and run the Alter method.  
$svr.Configuration.ShowAdvancedOptions.ConfigValue = 0  
$svr.Configuration.Alter()  
  
#Display when the change takes place according to the IsDynamic property.  
If ($svr.Configuration.ShowAdvancedOptions.IsDynamic -eq $true)  
 {
   "Configuration option has been updated."  
 }  
Else  
 {  
    "Configuration option will be updated when SQL Server is restarted."  
 }  
```  
