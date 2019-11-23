---
title: 取得 SQL Server PowerShell 說明 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Help [PowerShell]
- Help [SQL Server], PowerShell
- PowerShell [SQL Server], help
ms.assetid: 968c316d-db83-4c24-8ea6-9f18736842f7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 705512f54feae3bf60317c18b8c260ef484abebc
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/23/2019
ms.locfileid: "72797882"
---
# <a name="get-help-sql-server-powershell"></a>Get Help SQL Server PowerShell
  有關使用適用於 Windows PowerShell 和指令程式之 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 提供者的資訊來源有幾個。 其中包括 Windows PowerShell 環境中可用的說明。  
  
## <a name="before-you-begin"></a>開始之前  
 若要了解 Windows PowerShell，請參閱 [Windows PowerShell 開始使用手冊](https://technet.microsoft.com/library/hh857337.aspx)。  
  
 如需 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Cmdlet 和提供者的概觀，請參閱 [SQL Server PowerShell](../powershell/sql-server-powershell.md)。  
  
### <a name="help-in-the-windows-powershell-environment"></a>Windows PowerShell 環境中的説明  
 您可以使用 **Get-Help** Cmdlet，在 Windows PowerShell 環境中取得說明。 **Get-Help** 提供 Windows PowerShell 語言的基本說明，以及 Windows PowerShell 中可用的各種 Cmdlet 和提供者。  
  
 如需使用 **Get-Help**之方式的詳細資訊，請參閱 [Get-Help：取得說明](https://go.microsoft.com/fwlink/?LinkId=102136)。  
  
### <a name="sql-server-powershell-provider-help"></a>SQL Server PowerShell 提供者說明  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell 提供者實作 SQLSERVER 虛擬磁碟機上的數個資料夾，例如 SQLSERVER:\SQL 和 SQLSERVER:\DAC 資料夾。 每一個資料夾都會與一個 SQL Server 管理能力物件模型有關聯。 雖然您可以列出與 SQL Server 路徑中每個節點相關聯的方法和屬性，但是無法在 PowerShell 環境中取得它們的說明。 如需含有相關聯程式設計參考連結之資料夾的表格，請參閱 [SQL Server PowerShell 提供者](../powershell/sql-server-powershell-provider.md)。  
  
### <a name="invoke-sqlcmd-help"></a>Invoke-Sqlcmd 說明  
 **Invoke-Sqlcmd** Cmdlet 會採用 **sqlcmd** 公用程式可執行的任何查詢或指令碼檔案作為輸入。 您可以使用 **Get-Help** 取得有關 **Invoke-Sqlcmd** 和其參數的資訊，但是不包含 **sqlcmd** 查詢的 **Get-Help** 。  
  
 *-Query* 或 *-QueryFromFile* 輸入可包含：  
  
-   **sqlcmd** 變數和命令。 如需這些變數和命令的資訊，請參閱 [sqlcmd 公用程式](../tools/sqlcmd-utility.md)的＜備註＞一節。  
  
-   [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式。 如需 [!INCLUDE[tsql](../includes/tsql-md.md)] 語言的詳細資訊，請參閱 [Transact-SQL 參考 &#40;Database Engine&#41;](/sql/t-sql/language-reference)。  
  
-   XQuery 陳述式。 如需 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 所支援之 XQuery 語言的詳細資訊，請參閱 [XQuery 語言參考 &#40;SQL Server&#41;](/sql/xquery/xquery-language-reference-sql-server)。  
  
## <a name="get-help-for-a-sql-server-cmdlet"></a>取得 SQL Server Cmdlet 的説明  
 **取得 Cmdlet 的説明**  
  
-   指定 Cmdlet 的名稱以及要傳回的說明層級，以執行 Get-Help。  
  
### <a name="example-cmdlet-get-help"></a>範例：Get-Help Cmdlet  
 下列範例傳回 **Invoke-Sqlcmd**的各種說明層級：  
  
```powershell
## Get the basic help.  
Get-Help Invoke-Sqlcmd  
  
## Get the full help.  
Get-Help Invoke-Sqlcmd -Full  
  
## Get the parameter descriptions.  
Get-Help Invoke-Sqlcmd -Parameter *  
  
## Get the code examples.  
Get-Help Invoke-Sqlcmd -Examples  
  
## Get the syntax diagram.  
Get-Help Invoke-Sqlcmd -Syntax  
```  
  
## <a name="get-a-list-of-providers"></a>取得提供者清單  

### <a name="to-get-a-list-of-active-providers"></a>取得作用中的提供者清單
  
1.  指定提供者類別目錄，以執行 Get-Help。  
  
 如需在 Windows PowerShell 中取得提供者說明的詳細資訊，請參閱 [磁碟機和提供者](https://go.microsoft.com/fwlink/?LinkId=102137)。  
  
### <a name="example-get-a-list-of-providers"></a>範例：取得提供者清單  
 此程式碼會傳回目前在 Windows PowerShell 工作階段中啟用的提供者清單：  
  
```powershell
Get-Help -Category provider  
```  
  
## <a name="get-help-about-the-sql-server-provider"></a>取得 SQL Server 提供者的說明  
 **取得提供者的相關說明**  
  
1.  指定名稱 SQLServer，以執行 Get-Help  
  
### <a name="example-get-sql-server-provider-help"></a>範例：取得 SQL Server 提供者說明  
 此範例會傳回 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 提供者的基本資訊：  
  
```powershell
Get-Help SQLServer  
```  
  
## <a name="list-methods-and-properties"></a>列出方法和屬性  
 **列出 SQL Server 提供者路徑中節點的方法和屬性**  
  
1.  CD (切換) 至 SQL Server 路徑中的節點，或建立該位置的變數集。  
  
2.  以-Type 參數設定為方法或屬性來執行**取得成員**Cmdlet  
  
### <a name="examples-listing-methods-and-properties"></a>範例：列出方法與屬性  
 此範例列出 Databases 節點所支援的方法：  
  
```powershell
Set-Location SQL:\MyComputer\DEFAULT\Databases  
Get-Item . | Get-Member -Type Methods  
```  
  
 此範例列出已設為 SMO 資料表物件之變數的屬性：  
  
```powershell
$MyVar = New-Object Microsoft.SqlServer.Management.SMO.Table  
$MyVar | Get-Member -Type Properties  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server PowerShell 提供者](../powershell/sql-server-powershell-provider.md)   
 [使用 Database Engine Cmdlet](../../2014/database-engine/use-the-database-engine-cmdlets.md)  
