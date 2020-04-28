---
title: 針對擴充事件使用 PowerShell 提供者 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xevents
ms.topic: conceptual
helpviewer_keywords:
- PowerShell [SQL Server], xevent
- extended events [SQL Server], PowerShell
- PowerShell [SQL Server], extended events
ms.assetid: 0b10016f-a479-4444-a484-46cb4677cf64
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ea4432b07007ce1bbc4ec5b944594b204a7ad808
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "72782911"
---
# <a name="use-the-powershell-provider-for-extended-events"></a>針對擴充事件使用 PowerShell 提供者
  您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 提供者來管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 擴充事件。 XEvent 子資料夾位於 SQLSERVER 磁碟機底下。 您可以使用下列其中一種方法來存取這個資料夾：  
  
-   在命令提示字元中輸入 `sqlps`，然後按下 ENTER。 輸入 `cd xevent`，然後按 ENTER 鍵。 從該處，您可以使用**cd**和`dir`命令（或**設定位置**和**get-childitem** Cmdlet）來流覽至伺服器名稱和實例名稱。  
  
-   在物件總管中，展開執行個體名稱、展開 [管理]****、以滑鼠右鍵按一下 [擴充事件]****，然後按一下 [啟動 PowerShell]****。 這樣就會在下列路徑中啟動 PowerShell：  
  
     PS SQLSERVER： \ XEvent\\*ServerName*\\*實例*名稱>  
  
    > [!NOTE]  
    >  您可以從 [擴充事件]**** 底下的任何節點啟動 PowerShell。 例如，您可以用滑鼠右鍵按一下 [工作階段]****，然後按一下 [啟動 PowerShell]****。 這樣就會在下一個層級 (Sessions 資料夾) 啟動 PowerShell。  
  
 您可以瀏覽 XEvent 資料夾樹狀目錄來檢視現有的擴充事件工作階段及其相關聯的事件、目標和述詞。 例如，從 PS SQLSERVER： \ XEvent\\*ServerName*\\*InstanceName*> 路徑，如果您輸入`cd sessions`，請按 enter，輸入`dir`，然後按 enter 鍵，即可看到儲存在該實例上的會話清單。 您也可以檢視工作階段是否正在執行 (如果有，執行的時間長度)，以及工作階段是否設定為在執行個體啟動時啟動。  
  
 若要檢視與工作階段相關聯的事件、其述詞和目標，您可以將目錄變更為工作階段名稱，然後檢視 events 或 targets 資料夾。 例如，若要查看與預設系統健全狀況會話相關聯的事件及其述詞，請從 PS SQLSERVER： \ XEvent\\*ServerName*\\*InstanceName*\Sessions> 路徑，輸入`cd system_health\events,`按 enter 鍵，輸入`dir`，然後按 enter。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 提供者是一項功能強大的工具，可讓您用來建立、改變和管理擴充事件工作階段。 下列章節將提供使用 PowerShell 指令碼搭配擴充事件的一些基本範例。  
  
## <a name="examples"></a>範例  
 在下列範例中，請注意：  
  
-   腳本必須從 PS SQLSERVER：\\> 提示字元中執行（可在命令提示`sqlps`字元中輸入）。  
  
-   這些指令碼會使用預設 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體。  
  
-   您必須使用 .ps1 副檔名來儲存這些指令碼。  
  
-   PowerShell 執行原則必須允許指令碼執行。 若要設定執行原則，請使用 **Set-Executionpolicy** Cmdlet。 (如需詳細資訊，請輸入 `get-help set-executionpolicy -detailed`，然後按 ENTER 鍵。)  
  
 下列指令碼會建立名為 'TestSession' 的新工作階段。  
  
```powershell
#Script for creating a session.  
cd XEvent  
$h = hostname  
cd $h  
  
#Use the default instance.  
$store = dir | where {$_.DisplayName -ieq 'default'}  
$session = New-Object Microsoft.SqlServer.Management.XEvent.Session -ArgumentList $store, "TestSession"  
$event = $session.AddEvent("sqlserver.file_written")  
$event.AddAction("package0.callstack")  
$session.Create()  
```  
  
 下列指令碼會將信號緩衝區目標加入至您在上一則範例中建立的工作階段 (此範例會示範如何使用 `Alter` 方法。 請注意，當您第一次建立工作階段時，可以加入目標)。  
  
```powershell
#Script to alter a session.  
cd XEvent  
$h = hostname  
cd $h  
cd DEFAULT\Sessions  
  
#Used to find the specified session.  
$session = dir | where {$_.Name -eq 'TestSession'}  
  
#Add the ring buffer target and call the Alter method.  
$session.AddTarget("package0.ring_buffer")  
$session.Alter()  
```  
  
 下列指令碼會建立使用述詞運算式的新工作階段。 在此情況下，工作階段會收集何時寫入 c:\temp.log 檔案 (透過 sqlserver.file_written 事件) 的相關資訊。  
  
```powershell
#Script for creating a session.  
cd XEvent  
$h = hostname  
cd $h  
  
#Use the default instance.  
$store = dir | where {$_.DisplayName -ieq 'default'}  
$session = New-Object Microsoft.SqlServer.Management.XEvent.Session -ArgumentList $store, "TestSession2"  
$event = $session.AddEvent("sqlserver.file_written")  
  
#Construct a predicate "equal_i_unicode_string(path, N'c:\temp.log')".  
$column = $store.SqlServerPackage.EventInfoSet["file_written"].DataEventColumnInfoSet["path"]  
$operand = new-object Microsoft.SqlServer.Management.XEvent.PredOperand -argumentlist $column  
$value = new-object Microsoft.SqlServer.Management.XEvent.PredValue -argumentlist "c:\temp.log"  
$compare = $store.Package0Package.PredCompareInfoSet["equal_i_unicode_string"]  
$predicate = new-object Microsoft.SqlServer.Management.XEvent.PredFunctionExpr -ArgumentList $compare, $operand, $value  
$event.SetPredicate($predicate)  
$session.Create()  
```  
  
## <a name="security"></a>安全性  
 若要建立、更改或卸除擴充事件工作階段，您必須擁有 ALTER ANY EVENT SESSION 權限。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server PowerShell](../../powershell/sql-server-powershell.md)   
 [使用 system_health 會話](use-the-ssms-xe-profiler.md)   
 [擴充事件工具](extended-events-tools.md)  
