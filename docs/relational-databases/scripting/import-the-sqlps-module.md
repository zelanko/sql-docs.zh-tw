---
title: "匯入 SQLPS 模組 | Microsoft Docs"
ms.custom: 
ms.date: 08/01/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a972c56e-b2af-4fe6-abbd-817406e2c93a
caps.latest.revision: "12"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: cbd6691bf8fab45e58b41ad8e78166dd425ba605
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="import-the-sqlps-module"></a>匯入 SQLPS 模組
  從 PowerShell 管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的建議方式是將 **sqlps** 模組匯入 Windows PowerShell 環境中。 此模組會載入及註冊 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 嵌入式管理單元和管理能力組件。  從 Windows PowerShell 3.0 開始，模組會在命令中使用模組中的任何 Cmdlet 或函數時自動匯入。 這項功能適用於包含在 PSModulePath 環境變數值的目錄中的任何模組。  如需詳細資訊，請參閱 [匯入 PowerShell 模組](https://msdn.microsoft.com/library/dd878284(v=vs.85).aspx)
  
1.  **開始之前**  [安全性](#Security)  
  
2.  **載入模組**  [載入 sqlps 模組](#LoadSqlps)  
  
## <a name="before-you-begin"></a>開始之前  
 將 **sqlps** 模組匯入 Windows PowerShell 之後，即可：  
  
-   以互動方式執行 Windows PowerShell 命令。  
  
-   執行 Windows PowerShell 指令碼檔案。  
  
-   執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 指令程式。  
  
-   使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供者路徑來逐一導覽 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件的階層。  
  
-   使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理能力物件模型 (例如 Microsoft.SqlServer.Management.Smo) 來管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件。  
  
> [!NOTE]  
>  兩個 SQL Server Cmdlet (**Encode-Sqlname** 和 **Decode-Sqlname**) 名稱中所用的動詞，與核准的 Windows PowerShell 動詞不相符。 這不會影響其作業，但是 Windows PowerShell 會在將 **sqlps** 模組匯入工作階段時引發警告。  
  
###  <a name="Security"></a> 安全性  
 根據預設，Windows PowerShell 執行時會將指令碼執行原則設定為 [受限制]，這樣就不會執行任何 Windows PowerShell 指令碼。 若要載入 **sqlps** 模組您可以使用 **Set-ExecutionPolicy** Cmdlet 來允許執行已簽署的指令碼或任何指令碼。 建議您只執行來自信任來源的指令碼，並且利用適當的 NTFS 權限來保護所有輸入檔和輸出檔的安全。 如需啟用 Windows PowerShell 指令碼的詳細資訊，請參閱 [Running Windows PowerShell Scripts](http://www.microsoft.com/technet/scriptcenter/topics/winpsh/manual/run.mspx)(執行 Windows PowerShell 指令碼)。  
  
##  <a name="LoadSqlps"></a> 載入 sqlps 模組  
 **在 Windows PowerShell 中載入 sqlps 模組**  
  
1.  使用 **Set-ExecutionPolicy** Cmdlet，設定適當的指令碼執行原則。  
  
2.  使用 **Import-Module** Cmdlet，匯入 sqlps 模組。 如果您想要隱藏 **Encode-Sqlname** 和 **Decode-Sqlname** 的警告，請指定 **DisableNameChecking**參數。  
  
### <a name="example"></a>範例  
 此範例載入已關閉名稱檢查的 **sqlps** 模組。  
  
```powershell 
# Import the SQL Server Module.    
Import-Module Sqlps -DisableNameChecking;

# To check whether the module is installed.
Get-Module -ListAvailable -Name Sqlps;
```  
  
> [!NOTE]  
>  如果 **sqlps** 模組不在路徑中，請變更模組的位置或在指令碼中使用完整路徑 (在有空格之路徑中使用加上雙引號的資料夾名稱)。 **sqlps** 模組位於 SQL Server 執行個體的 Tools\Powershell 資料夾中。  
  
 ![搭配 [回到頁首] 連結使用的箭號圖示](../../analysis-services/instances/media/uparrow16x16.gif "搭配 [回到頁首] 連結使用的箭號圖示") [&#91;頂端&#93;]()  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)   
 [SQL Server PowerShell 提供者](../../relational-databases/scripting/sql-server-powershell-provider.md)   
 [使用 Database Engine Cmdlet](../../relational-databases/scripting/use-the-database-engine-cmdlets.md)  
 [安裝 PowerShell 模組](https://msdn.microsoft.com/library/dd878350(v=vs.85).aspx)  
 [Import-Module](https://technet.microsoft.com/library/hh849725.aspx)
  
  
