---
title: "載入 Windows PowerShell 中的 SMO 組件 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8ca42b69-da5a-47f4-9085-34e443f0e389
caps.latest.revision: 9
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 149ba0be18c46dbf2171f7a1fac0641ae81d3515
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="load-the-smo-assemblies-in-windows-powershell"></a>載入 Windows PowerShell 中的 SMO 組件
  此主題描述如何在未使用 SQL Server PowerShell 提供者的 Windows PowerShell 指令碼中載入 SQL Server 管理物件 (SMO) 組件。  
  
## <a name="before-you-begin"></a>開始之前  
 載入 SMO 組件的慣用機制是載入 **sqlps** 模組。 模組中所含的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供者會自動載入 SMO 組件，也會實作可擴充 PowerShell 指令碼中 SMO 物件使用性的功能。  如需詳細資訊，請參閱 [匯入 SQLPS 模組](../../relational-databases/scripting/import-the-sqlps-module.md)。
  
 有兩種情況您可能必須直接載入 SMO 組件：  
  
-   如果您的指令碼在第一個命令之前先參考 SMO 物件，而該命令會從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 嵌入式管理單元參考提供者或指令程式。  
  
-   您想要從不使用提供者或 Cmdlet 的另一個語言 (例如 C# 或 Visual Basic) 移植 SMO 程式碼。  
  
## <a name="example-loading-the-sql-server-management-objects"></a>範例：載入 SQL Server 管理物件  
 下列程式碼會載入 SMO 組件：  
  
```  
#  
# Loads the SQL Server Management Objects (SMO)  
#  
  
$ErrorActionPreference = "Stop"  
  
$sqlpsreg="HKLM:\SOFTWARE\Microsoft\PowerShell\1\ShellIds\Microsoft.SqlServer.Management.PowerShell.sqlps"  
  
if (Get-ChildItem $sqlpsreg -ErrorAction "SilentlyContinue")  
{  
    throw "SQL Server Provider for Windows PowerShell is not installed."  
}  
else  
{  
    $item = Get-ItemProperty $sqlpsreg  
    $sqlpsPath = [System.IO.Path]::GetDirectoryName($item.Path)  
}  
  
$assemblylist =   
"Microsoft.SqlServer.Management.Common",  
"Microsoft.SqlServer.Smo",  
"Microsoft.SqlServer.Dmf ",  
"Microsoft.SqlServer.Instapi ",  
"Microsoft.SqlServer.SqlWmiManagement ",  
"Microsoft.SqlServer.ConnectionInfo ",  
"Microsoft.SqlServer.SmoExtended ",  
"Microsoft.SqlServer.SqlTDiagM ",  
"Microsoft.SqlServer.SString ",  
"Microsoft.SqlServer.Management.RegisteredServers ",  
"Microsoft.SqlServer.Management.Sdk.Sfc ",  
"Microsoft.SqlServer.SqlEnum ",  
"Microsoft.SqlServer.RegSvrEnum ",  
"Microsoft.SqlServer.WmiEnum ",  
"Microsoft.SqlServer.ServiceBrokerEnum ",  
"Microsoft.SqlServer.ConnectionInfoExtended ",  
"Microsoft.SqlServer.Management.Collector ",  
"Microsoft.SqlServer.Management.CollectorEnum",  
"Microsoft.SqlServer.Management.Dac",  
"Microsoft.SqlServer.Management.DacEnum",  
"Microsoft.SqlServer.Management.Utility"  
  
foreach ($asm in $assemblylist)  
{  
    $asm = [Reflection.Assembly]::LoadWithPartialName($asm)  
}  
  
Push-Location  
cd $sqlpsPath  
update-FormatData -prependpath SQLProvider.Format.ps1xml   
Pop-Location  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)  
  
  

