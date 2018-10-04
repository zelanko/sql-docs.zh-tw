---
title: 使用 WMI 提供者來管理服務和網路設定 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- WMI provider [SMO]
- services [SQL Server], SMO
- network settings [SMO]
- monitoring [SMO]
ms.assetid: ef8c3986-1098-4f21-b03a-f1f6bdb51c26
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: dc42cd7c5f7670ed3ece73ee424de03891ed5781
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48211658"
---
# <a name="managing-services-and-network-settings-by-using-wmi-provider"></a>使用 WMI 提供者管理服務和網路設定
  WMI 提供者是已發行的介面，以供[!INCLUDE[msCoName](../../../includes/msconame-md.md)]Management Console (MMC) 來管理[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]服務和網路通訊協定。 在 SMO 中，<xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer>物件都代表 WMI 提供者。  
  
 <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer>物件操作可建立的連線與不同<xref:Microsoft.SqlServer.Management.Smo.Server>物件的執行個體[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，並使用 Windows 認證來連接到 WMI 服務。  
  
## <a name="example"></a>範例  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
 程式使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]WMI 提供者，您必須包含`Imports`陳述式來限定 WMI 命名空間。 將陳述式插入至其他 `Imports` 陳述式之後、在應用程式中的任何宣告之前，例如：  
  
 `Imports Microsoft.SqlServer.Management.Smo`  
  
 `Imports Microsoft.SqlServer.Management.Common`  
  
 `Imports Microsoft.SqlServer.Management.Smo.Wmi`  
  
## <a name="stopping-and-restarting-the-microsoft-sql-server-service-to-the-instance-of-sql-server-in-visual-basic"></a>在 Visual Basic 中對 SQL Server 的執行個體停止和重新啟動 Microsoft SQL Server 服務  
 此程式碼範例示範如何使用 SMO <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> 物件停止和啟動服務。 如此可為 WMI 提供者提供組態管理的介面。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBWMIService1](SMO How to#SMO_VBWMIService1)]  -->  
  
## <a name="enabling-a-server-protocol-using-a-urn-string-in-visual-basic"></a>在 Visual Basic 中使用 URN 字串啟用伺服器通訊協定  
 這個程式碼範例示範如何使用 URN 物件辨識伺服器通訊協定，然後啟用該通訊協定。  
  
```  
'This program must run with administrator privileges.  
        'Declare the ManagedComputer WMI interface.  
        Dim mc As New ManagedComputer()  
  
        'Create a URN object that represents the TCP server protocol.  
        Dim u As New Urn("ManagedComputer[@Name='V-ROBMA3']/ServerInstance[@Name='MSSQLSERVER']/ServerProtocol[@Name='Tcp']")  
  
        'Declare the serverProtocol variable and return the ServerProtocol object.  
        Dim sp As ServerProtocol  
        sp = mc.GetSmoObject(u)  
  
        'Enable the protocol.  
        sp.IsEnabled = True  
  
        'propagate back to the service  
        sp.Alter()  
```  
  
## <a name="enabling-a-server-protocol-using-a-urn-string-in-powershell"></a>在 PowerShell 中使用 URN 字串啟用伺服器通訊協定  
 這個程式碼範例示範如何使用 URN 物件辨識伺服器通訊協定，然後啟用該通訊協定。  
  
```  
#This example shows how to identify a server protocol using a URN object, and then enable the protocol  
#This program must run with administrator privileges.  
  
#Load the assembly containing the classes used in this example  
[reflection.assembly]::LoadWithPartialName("Microsoft.SqlServer.SqlWmiManagement")  
  
#Get a managed computer instance  
$mc = New-Object -TypeName Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer  
  
#Create a URN object that represents the TCP server protocol  
#Change 'MyPC' to the name of the your computer   
$urn = New-Object -TypeName Microsoft.SqlServer.Management.Sdk.Sfc.Urn -argumentlist "ManagedComputer[@Name='MyPC']/ServerInstance[@Name='MSSQLSERVER']/ServerProtocol[@Name='Tcp']"  
  
#Get the protocol object  
$sp = $mc.GetSmoObject($urn)  
  
#enable the protocol on the object  
$sp.IsEnabled = $true  
  
#propagate back to actual service  
$sp.Alter()  
```  
  
## <a name="starting-and-stopping-a-service-in-visual-c"></a>在 Visual C# 中啟動和停止服務  
 此程式碼範例示範如何停止和啟動 SQL Server 的執行個體。  
  
```  
{   
   //Declare and create an instance of the ManagedComputer   
   //object that represents the WMI Provider services.   
   ManagedComputer mc;   
   mc = new ManagedComputer();   
   //Iterate through each service registered with the WMI Provider.   
  
   foreach (Service svc in mc.Services)  
   {   
      Console.WriteLine(svc.Name);   
   }   
//Reference the Microsoft SQL Server service.   
  Service Mysvc = mc.Services["MSSQLSERVER"];   
//Stop the service if it is running and report on the status  
// continuously until it has stopped.   
   if (Mysvc.ServiceState == ServiceState.Running) {   
      Mysvc.Stop();   
      Console.WriteLine(string.Format("{0} service state is {1}", Mysvc.Name, Mysvc.ServiceState));   
      while (!(string.Format("{0}", Mysvc.ServiceState) == "Stopped")) {   
         Console.WriteLine(string.Format("{0}", Mysvc.ServiceState));   
          Mysvc.Refresh();   
      }   
      Console.WriteLine(string.Format("{0} service state is {1}", Mysvc.Name, Mysvc.ServiceState));   
//Start the service and report on the status continuously   
//until it has started.   
      Mysvc.Start();   
      while (!(string.Format("{0}", Mysvc.ServiceState) == "Running")) {   
         Console.WriteLine(string.Format("{0}", Mysvc.ServiceState));   
         Mysvc.Refresh();   
      }   
      Console.WriteLine(string.Format("{0} service state is {1}", Mysvc.Name, Mysvc.ServiceState));  
      Console.ReadLine();  
   }   
   else {   
      Console.WriteLine("SQL Server service is not running.");  
      Console.ReadLine();  
   }   
}  
```  
  
## <a name="starting-and-stopping-a-service-in-powershell"></a>在 PowerShell 中啟動和停止服務  
 此程式碼範例示範如何停止和啟動 SQL Server 的執行個體。  
  
```  
#Load the assembly containing the objects used in this example  
[reflection.assembly]::LoadWithPartialName("Microsoft.SqlServer.SqlWmiManagement")  
  
#Get a managed computer instance  
$mc = New-Object -TypeName Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer  
  
#List out all sql server instnces running on this mc  
foreach ($Item in $mc.Services){$Item.Name}  
  
#Get the default sql server datbase engine service  
$svc = $mc.Services["MSSQLSERVER"]  
  
# for stopping and starting services PowerShell must run as administrator  
  
#Stop this service  
$svc.Stop()  
$svc.Refresh()  
while ($svc.ServiceState -ne "Stopped")  
{  
$svc.Refresh()  
$svc.ServiceState  
}  
"Service" + $svc.Name + " is now stopped"  
"Starting " + $svc.Name  
$svc.Start()  
$svc.Refresh()  
while ($svc.ServiceState -ne "Running")  
{  
$svc.Refresh()  
$svc.ServiceState  
}  
$svc.ServiceState  
"Service" + $svc.Name + "is now started"  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [組態管理的 WMI 提供者概念](../../wmi-provider-configuration/wmi-provider-for-configuration-management.md)  
  
  
