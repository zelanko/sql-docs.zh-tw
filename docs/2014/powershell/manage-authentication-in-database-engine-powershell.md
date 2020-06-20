---
title: 管理資料庫引擎 PowerShell 中的驗證 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: ab9212a6-6628-4f08-a38c-d3156e05ddea
author: stevestein
ms.author: sstein
ms.openlocfilehash: cd9919b17e0422a9308e36cd1befb6865a67ff67
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84960398"
---
# <a name="manage-authentication-in-database-engine-powershell"></a>管理 Database Engine PowerShell 中的驗證
  依預設，連接至 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的執行個體時， [!INCLUDE[ssDE](../includes/ssde-md.md)]PowerShell 元件會使用 Windows 驗證。 藉由定義 PowerShell 虛擬磁碟機，或指定 `-Username` 的 `-Password` 和 `Invoke-Sqlcmd` 參數，即可使用 SQL Server 驗證。  
  
1.  **Before you begin:**  [Permissions](#Permissions)  
  
2.  **使用下列項目，設定驗證：**  [虛擬磁碟機](#SQLAuthVirtDrv)、[Invoke-Sqlcmd](#SQLAuthInvSqlCmd)  
  
##  <a name="permissions"></a><a name="Permissions"></a> 權限  
 您在 [!INCLUDE[ssDE](../includes/ssde-md.md)] 的執行個體中可執行的所有動作，都是透過授與用來連接至執行個體之驗證認證的權限所控制。 依預設， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 提供者和 Cmdlet 會使用用來建立 [!INCLUDE[ssDE](../includes/ssde-md.md)]之 Windows 驗證連接的 Windows 帳戶。  
  
 若要進行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證連接，您必須提供 SQL Server 驗證登入識別碼和密碼。 使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 提供者時，您必須將 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 登入認證與虛擬磁片磁碟機產生關聯，然後使用變更目錄命令（ `cd` ）連接到該磁片磁碟機。 在 Windows PowerShell 中，安全性認證只能與虛擬磁碟機產生關聯。  
  
##  <a name="sql-server-authentication-using-a-virtual-drive"></a><a name="SQLAuthVirtDrv"></a> 使用虛擬磁碟機的 SQL Server 驗證  
 **建立與 SQL Server 驗證登入相關聯的虛擬磁碟機**  
  
1.  建立的函數：  
  
    1.  具有參數可表示提供給虛擬磁碟機的名稱、登入識別碼，以及與虛擬磁碟機相關聯的提供者路徑。  
  
    2.  使用 `read-host` 提示使用者輸入密碼。  
  
    3.  使用 `new-object` 建立認證物件。  
  
    4.  使用 `new-psdrive` 建立具有已提供認證的虛擬磁碟機。  
  
2.  呼叫此函數，以建立具有已提供認證的虛擬磁碟機。  
  
### <a name="example-virtual-drive"></a>範例 (虛擬磁碟機)  
 此範例會建立名為 **sqldrive** 的函數，可讓您用來建立與指定之 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證登入和執行個體相關聯的虛擬磁碟機。  
  
 **sqldrive** 函數會提示您輸入登入的密碼，並且在您輸入時遮罩密碼。 然後，每當您使用變更目錄命令（ `cd` ）連接到使用虛擬磁片磁碟機名稱的路徑時，就會使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 您在建立磁片磁碟機時所提供的驗證登入認證來執行所有作業。  
  
```powershell
## Create a function that specifies the login and prompts for the password.  
  
function sqldrive  
{  
    param( [string]$name, [string]$login = "MyLogin", [string]$root = "SQLSERVER:\SQL\MyComputer\MyInstance" )  
    $pwd = Read-Host -AsSecureString -Prompt "Password"  
    $cred = New-Object System.Management.Automation.PSCredential -argumentlist $login, $pwd  
    New-PSDrive $name -PSProvider SqlServer -Root $root -Credential $cred -Scope 1  
}  
  
## Use the sqldrive function to create a SQLAuth virtual drive.  
sqldrive SQLAuth  
  
## CD to the virtual drive, which invokes the supplied authentication credentials.  
cd SQLAuth  
```  
  
##  <a name="sql-server-authentication-using-invoke-sqlcmd"></a><a name="SQLAuthInvSqlCmd"></a> 使用 Invoke-Sqlcmd 的 SQL Server 驗證  
 **搭配使用 Invoke-Sqlcmd 與 SQL Server 驗證**  
  
1.  使用 `-Username` 參數指定登入識別碼，而 `-Password` 參數則可指定相關聯的密碼。  
  
### <a name="example-invoke-sqlcmd"></a>範例 (Invoke-Sqlcmd)  
 此範例使用 read-host Cmdlet 提示使用者輸入密碼，然後使用 SQL Server 驗證進行連接。  
  
```powershell
## Prompt the user for their password.  
$pwd = Read-Host -AsSecureString -Prompt "Password"  
  
Invoke-Sqlcmd -Query "SELECT GETDATE() AS TimeOfQuery;" -ServerInstance "MyComputer\MyInstance" -Username "MyLogin" -Password $pwd  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server PowerShell](sql-server-powershell.md)   
 [SQL Server PowerShell 提供者](sql-server-powershell-provider.md)   
 [Invoke-Sqlcmd 指令程式](../database-engine/invoke-sqlcmd-cmdlet.md)  
