---
title: 載入 Windows PowerShell 中的 SMO 組件 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: scripting
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 8ca42b69-da5a-47f4-9085-34e443f0e389
caps.latest.revision: 9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 598dc8bdecdfaad0e685b0da5d57f41c8c52f052
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2018
---
# <a name="load-the-smo-assemblies-in-windows-powershell"></a>載入 Windows PowerShell 中的 SMO 組件
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

本文描述如何在未使用 SQL Server PowerShell 提供者的 Windows PowerShell 指令碼中載入 SQL Server 管理物件 (SMO) 組件。  
  
> [!NOTE]
> 有兩個 SQL Server PowerShell 模組：**SqlServer** 和 **SQLPS**。 **SQLPS** 模組隨附於 SQL Server 安裝 (基於回溯相容性)，但不再更新。 最新版 PowerShell 模組是 **SqlServer** 模組。 **SqlServer** 模組包含 **SQLPS** 中 Cmdlet 的更新版本，此外還加入新的 Cmdlet 以支援最新版 SQL 功能。  
> 舊版 **SqlServer** 模組隨附於 SQL Server Management Studio (SSMS)，但僅限 SSMS 16.x 版。 若要搭配 SSMS 17.0 和更新版本使用 PowerShell，則必須從 PowerShell 資源庫安裝 **SqlServer** 模組。
> 若要安裝 **SqlServer** 模組，請參閱[安裝 SQL Server PowerShell](download-sql-server-ps-module.md)。


載入 SMO 組件的慣用機制是載入 **SqlServer** 模組。 模組中所含的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 提供者會自動載入 SMO 組件，也會實作可擴充 PowerShell 指令碼中 SMO 物件使用性的功能。
  
有兩種情況您可能必須直接載入 SMO 組件：  
  
-   如果您的指令碼在第一個命令之前先參考 SMO 物件，而該命令會從 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 嵌入式管理單元參考提供者或指令程式。  
  
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
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  
