---
title: 匯入 SQLPS 模組 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a972c56e-b2af-4fe6-abbd-817406e2c93a
caps.latest.revision: 9
author: mgblythe
ms.author: mblythe
manager: jhubbard
ms.openlocfilehash: 8c20daf51270931609fb876b9a7035da343d19f7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36036173"
---
# <a name="import-the-sqlps-module"></a>匯入 SQLPS 模組
  從 PowerShell 管理 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的建議方式是將 `sqlps` 模組匯入 Windows PowerShell 2.0 環境中。 此模組會載入及註冊 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 嵌入式管理單元和管理能力組件。  
  
1.  **開始之前**：[安全性](#Security)  
  
2.  **載入模組**  [載入 sqlps 模組](#LoadSqlps)  
  
## <a name="before-you-begin"></a>開始之前  
 將 `sqlps` 模組匯入 Windows PowerShell 之後，即可：  
  
-   以互動方式執行 Windows PowerShell 命令。  
  
-   執行 Windows PowerShell 指令碼檔案。  
  
-   執行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 指令程式。  
  
-   使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 提供者路徑來逐一導覽 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 物件的階層。  
  
-   使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 管理能力物件模型 (例如 Microsoft.SqlServer.Management.Smo) 來管理 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 物件。  
  
> [!NOTE]  
>  兩個 SQL Server Cmdlet (`Encode-Sqlname` 和 `Decode-Sqlname`) 名稱中所用的動詞，與核准的 Windows PowerShell 2.0 動詞不相符。 這不會影響其作業，但是 Windows PowerShell 會引發警告時`sqlps`模組匯入工作階段。  
  
###  <a name="Security"></a> 安全性  
 根據預設，Windows PowerShell 執行時會將指令碼執行原則設定為 [受限制]，這樣就不會執行任何 Windows PowerShell 指令碼。 若要載入 `sqlps` 模組，您可以使用 `Set-ExecutionPolicy` Cmdlet 來允許執行已簽署的指令碼或任何指令碼。 建議您只執行來自信任來源的指令碼，並且利用適當的 NTFS 權限來保護所有輸入檔和輸出檔的安全。 如需啟用 Windows PowerShell 指令碼的詳細資訊，請參閱 [Running Windows PowerShell Scripts](http://www.microsoft.com/technet/scriptcenter/topics/winpsh/manual/run.mspx)(執行 Windows PowerShell 指令碼)。  
  
##  <a name="LoadSqlps"></a> 載入 sqlps 模組  
 **在 Windows PowerShell 中載入 sqlps 模組**  
  
1.  使用`Set-ExecutionPolicy`cmdlet，設定適當的指令碼執行原則。  
  
2.  使用`Import-Module`cmdlet 匯入 sqlps 模組。 指定`DisableNameChecking`參數，如果您想要隱藏警告的相關`Encode-Sqlname`和`Decode-Sqlname`。  
  
### <a name="example-powershell"></a>範例 (PowerShell)  
 此範例載入已關閉名稱檢查的 `sqlps` 模組。  
  
```  
## Import the SQL Server Module.  
  
Import-Module “sqlps” -DisableNameChecking  
  
```  
  

  
## <a name="see-also"></a>另請參閱  
 [SQL Server PowerShell](../powershell/sql-server-powershell.md)   
 [SQL Server PowerShell 提供者](../powershell/sql-server-powershell-provider.md)   
 [使用資料庫引擎 Cmdlet](../../2014/database-engine/use-the-database-engine-cmdlets.md)  
  
  