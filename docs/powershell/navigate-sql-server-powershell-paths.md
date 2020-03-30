---
title: 導覽 SQL Server PowerShell 路徑 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: d68aca48-d161-45ed-9f4f-14122ed30218
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4ced679315a8e682a438f2ab99ca610219768172
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "68049123"
---
# <a name="navigate-sql-server-powershell-paths"></a>導覽 SQL Server PowerShell 路徑
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[ssDE](../includes/ssde-md.md)] PowerShell 提供者會公開一組物件，而這組物件位在類似於檔案路徑之結構的 SQL Server 執行個體中。 您可以使用 Windows PowerShell 指令程式導覽提供者路徑，以及建立自訂磁碟機來縮短必須輸入的路徑。  

> [!NOTE]
> 有兩個 SQL Server PowerShell 模組：**SqlServer** 和 **SQLPS**。 **SQLPS** 模組隨附於 SQL Server 安裝 (基於回溯相容性)，但不再更新。 最新版 PowerShell 模組是 **SqlServer** 模組。 **SqlServer** 模組包含 **SQLPS** 中 Cmdlet 的更新版本，此外還加入新的 Cmdlet 以支援最新版 SQL 功能。  
> 舊版 **SqlServer** 模組隨附於  SQL Server Management Studio (SSMS)，但僅限 SSMS 16.x 版。 若要搭配 SSMS 17.0 和更新版本使用 PowerShell，則必須從 PowerShell 資源庫安裝 **SqlServer** 模組。
> 若要安裝 **SqlServer** 模組，請參閱[安裝 SQL Server PowerShell](download-sql-server-ps-module.md)。
  
Windows PowerShell 實作指令程式以導覽路徑結構，而路徑結構代表 PowerShell 提供者所支援物件的階層。 在您導覽至路徑中的節點時，可以使用其他 Cmdlet 來執行目前物件的基本作業。 由於 Cmdlet 會經常被使用，所以具有簡短、標準的別名。 也有一組別名會將指令程式對應到類似的命令提示字元命令，而且有另一組別名適用於 UNIX Shell 命令。  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 提供者會實作提供者 Cmdlet 的子集，如下表所示：  
  
|Cmdlet|標準的別名|cmd 別名|UNIX Shell 別名|描述|  
|------------|---------------------|---------------|----------------------|-----------------|  
|**Get-Location**|**gl**|**pwd**|**pwd**|取得目前的節點。|  
|**Set-Location**|**sl**|**cd, chdir**|**cd, chdir**|變更目前的節點。|  
|**Get-ChildItem**|**gci**|**dir**|**ls**|列出儲存在目前節點上的物件。|  
|**Get-Item**|**gi**|||傳回目前項目的屬性。|  
|**Rename-Item**|**rni**|**rn**|**ren**|重新命名物件。|  
|**Remove-Item**|**ri**|**del, rd**|**rm, rmdir**|移除物件。|  
  
> [!IMPORTANT]  
>  某些 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 識別碼 (物件名稱) 包含 Windows PowerShell 在路徑名稱中不支援的字元。 如需如何使用包含這些字元之名稱的詳細資訊，請參閱 [PowerShell 中的 SQL Server 識別碼](sql-server-identifiers-in-powershell.md)。  
  
### <a name="sql-server-information-returned-by-get-childitem"></a>Get-ChildItem 所傳回的 SQL Server 資訊  
 **Get-ChildItem** (或其 **dir** 和 **ls** 別名) 傳回的資訊視您在 SQLSERVER: 路徑中的位置而定。  
  
|路徑位置|Get-ChildItem 結果|  
|-------------------|----------------------------|  
|SQLSERVER:\SQL|傳回本機電腦的名稱。 若您已經使用 SMO 或 WMI 連線到其他電腦上的 [!INCLUDE[ssDE](../includes/ssde-md.md)] 執行個體，也會列出這些電腦。|  
|SQLSERVER:\SQL\\*ComputerName*|電腦上 [!INCLUDE[ssDE](../includes/ssde-md.md)] 執行個體的清單。|  
|SQLSERVER:\SQL\\*ComputerName*\\*InstanceName*|執行個體中最上層物件類型的清單，例如 Endpoints、Certificates 和 Databases。|  
|物件類別節點，例如 Databases|該類型的物件清單，例如資料庫的清單：master、model、AdventureWorks20008R2。|  
|物件名稱節點，例如 AdventureWorks2012|此物件內所包含的物件類型清單。 例如，資料庫會列出資料表和檢視表之類的物件類型。|  
  
 **Get-ChildItem** 預設不會列出任何系統物件。 *Force* 參數可用來查看系統物件，例如 **sys** 結構描述中的物件。  
  
### <a name="custom-drives"></a>自訂磁碟機  
 Windows PowerShell 可讓使用者定義稱為 PowerShell 磁碟機的虛擬磁碟機。 這些磁碟機會透過路徑陳述式的開始節點進行對應。 它們通常是用來縮短經常輸入的路徑。 SQLSERVER: 路徑可能會很長，佔據 Windows PowerShell 視窗的空間且需要很長的鍵入。 若您要在特定路徑節點上執行很多工作，您可以定義可對應至該節點的自訂 Windows PowerShell 磁碟機。  
  
## <a name="use-powershell-cmdlet-aliases"></a>使用 PowerShell 指令程式別名  
 **使用 Cmdlet 別名**  
  
-   輸入較短的別名，或對應至熟悉命令提示字元命令的別名，而不要輸入完整 Cmdlet 名稱。  
  
### <a name="alias-example-powershell"></a>別名範例 (PowerShell)  
 例如，您可以使用下列其中一組 Cmdlet 或別名來擷取可用的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體清單，方式是導覽至 SQLSERVER:\SQL 資料夾，並要求該資料夾的子項目清單：  
  
```  
## Shows using the full cmdet name.  
Set-Location SQLSERVER:\SQL  
Get-ChildItem  
  
## Shows using canonical aliases.  
sl SQLSERVER:\SQL  
gci  
  
## Shows using command prompt aliases.  
cd SQLSERVER:\SQL  
dir  
  
## Shows using Unix shell aliases.  
cd SQLSERVER:\SQL  
ls  
```  
  
## <a name="use-get-childitem"></a>使用 Get-ChildItem  
 **使用 Get-ChildItem 傳回資訊**  
  
1.  巡覽至您要其子系清單的節點  
  
2.  執行 Get-Childitem 以取得清單。  
  
### <a name="get-childitem-example-powershell"></a>Get-ChildItem 範例 (PowerShell)  
 這些範例說明 Get-Childitem 針對 SQL Server 提供者路徑中不同節點所傳回的資訊。  
  
```  
## Return the current computer and any computer  
## to which you have made a SQL or WMI connection.  
Set-Location SQLSERVER:\SQL  
Get-ChildItem  
  
## List the instances of the Database Engine on the local computer.  
  
Set-Location SQLSERVER:\SQL\localhost  
Get-ChildItem  
  
## Lists the categories of objects available in the  
## default instance on the local computer.  
Set-Location SQLSERVER:\SQL\localhost\DEFAULT  
Get-ChildItem  
  
## Lists the databases from the local default instance.  
## The force parameter is used to include the system databases.  
Set-Location SQLSERVER:\SQL\localhost\DEFAULT\Databases  
Get-ChildItem -force  
```  
  
## <a name="create-a-custom-drive"></a>建立自訂磁碟機  
 **建立和使用自訂磁碟機**  
  
1.  您可以使用 **New-PSDrive** 定義自訂磁碟機。 您可以使用 **Root** 參數指定以自訂磁碟機名稱呈現的路徑。  
  
2.  參考路徑導覽 Cmdlet (例如 **Set-Location**) 中的自訂磁碟機名稱。  
  
### <a name="custom-drive-example-powershell"></a>自訂磁碟機範例 (PowerShell)  
 此範例會建立名為 AWDB 且對應至已部署 AdventureWorks2012 範例資料庫複本之節點的虛擬磁碟機。 然後，您可以使用虛擬磁碟機來導覽至資料庫中的資料表。  
  
```  
## Create a new virtual drive.  
New-PSDrive -Name AWDB -Root SQLSERVER:\SQL\localhost\DEFAULT\Databases\AdventureWorks2012  
  
## Use AWDB: to navigate to a specific table.  
Set-Location AWDB:\Tables\Purchasing.Vendor  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server PowerShell 提供者](sql-server-powershell-provider.md)   
 [使用 SQL Server PowerShell 路徑](work-with-sql-server-powershell-paths.md)   
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  
