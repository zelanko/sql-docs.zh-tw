---
title: 匯入 SQLPS 模組 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: a972c56e-b2af-4fe6-abbd-817406e2c93a
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 34859c0c516c61a73e31dbf752ab274188c6343a
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/23/2019
ms.locfileid: "72797866"
---
# <a name="import-the-sqlps-module"></a>匯入 SQLPS 模組
  從 PowerShell 管理 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的建議方式是將 `sqlps` 模組匯入 Windows PowerShell 2.0 環境中。 此模組會載入及註冊 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 嵌入式管理單元和管理能力組件。  
  
1.  **開始之前**：[安全性](#Security)  
  
2.  **To load the module:**  [Load the sqlps Module](#LoadSqlps)  
  
## <a name="before-you-begin"></a>開始之前  
 將 `sqlps` 模組匯入 Windows PowerShell 之後，即可：  
  
-   以互動方式執行 Windows PowerShell 命令。  
  
-   執行 Windows PowerShell 指令碼檔案。  
  
-   執行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 指令程式。  
  
-   使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 提供者路徑來逐一導覽 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 物件的階層。  
  
-   使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 管理能力物件模型 (例如 Microsoft.SqlServer.Management.Smo) 來管理 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 物件。  
  
> [!NOTE]  
>  兩個 SQL Server Cmdlet (`Encode-Sqlname` 和 `Decode-Sqlname`) 名稱中所用的動詞，與核准的 Windows PowerShell 2.0 動詞不相符。 這不會影響其作業，但是 Windows PowerShell 會在將 `sqlps` 模組匯入工作階段時引發警告。  
  
###  <a name="Security"></a> Security  
 根據預設，Windows PowerShell 執行時會將指令碼執行原則設定為 [受限制]，這樣就不會執行任何 Windows PowerShell 指令碼。 若要載入 `sqlps` 模組，您可以使用 `Set-ExecutionPolicy` Cmdlet 來允許執行已簽署的指令碼或任何指令碼。 建議您只執行來自信任來源的指令碼，並且利用適當的 NTFS 權限來保護所有輸入檔和輸出檔的安全。 如需啟用 Windows PowerShell 指令碼的詳細資訊，請參閱 [Running Windows PowerShell Scripts](https://docs.microsoft.com/powershell/scripting/setup/starting-windows-powershell?view=powershell-6#how-to-enable-windows-powershell-ise-on-earlier-releases-of-windows) (執行 Windows PowerShell 指令碼)。  
  
##  <a name="LoadSqlps"></a> 載入 sqlps 模組  

### <a name="to-load-the-sqlps-module-in-windows-powershell"></a>在 Windows PowerShell 中載入 sqlps 模組
  
1.  使用 `Set-ExecutionPolicy` Cmdlet，設定適當的指令碼執行原則。  
  
2.  使用 `Import-Module` Cmdlet，匯入 sqlps 模組。 如果您想要隱藏 `DisableNameChecking` 和 `Encode-Sqlname` 的警告，請指定 `Decode-Sqlname` 參數。  
  
### <a name="example-powershell"></a>範例 (PowerShell)  
 此範例載入已關閉名稱檢查的 `sqlps` 模組。  
  
```powershell
## Import the SQL Server Module.  
  
Import-Module "sqlps" -DisableNameChecking  
```  

## <a name="see-also"></a>另請參閱  
 [SQL Server PowerShell](../powershell/sql-server-powershell.md)   
 [SQL Server PowerShell 提供者](../powershell/sql-server-powershell-provider.md)   
 [使用 Database Engine Cmdlet](../../2014/database-engine/use-the-database-engine-cmdlets.md)  
