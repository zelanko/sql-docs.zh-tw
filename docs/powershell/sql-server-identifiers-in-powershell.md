---
title: PowerShell 中的 SQL Server 識別碼 | Microsoft Docs
description: 了解 Windows PowerShell 提供者用來公開資料階層的路徑，以及在這些路徑中編碼 PowerShell 所不支援特定字元的需求。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: sql-server-powershell
ms.topic: conceptual
helpviewer_keywords:
- Cmdlets [SQL Server], Encode-Sqlname
- PowerShell [SQL Server], identifiers
- Encode-Sqlname cmdlet
- PowerShell [SQL Server], Encode-Sqlname
- Decode-Sqlname cmdlet
- PowerShell [SQL Server], Decode-Sqlname
- identifiers [SQL Server], PowerShell
- Cmdlets [SQL Server], Decode-Sqlname
ms.assetid: 651099b0-33b4-453a-a864-b067f21eb8b9
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 54a37555038b3757ebff61faad8717c6a800ff1c
ms.sourcegitcommit: a9f16d7819ed0e2b7ad8f4a7d4d2397437b2bbb2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/21/2020
ms.locfileid: "88714296"
---
# <a name="sql-server-identifiers-in-powershell"></a>PowerShell 中的 SQL Server 識別碼
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

適用於 Windows PowerShell 的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 提供者會使用 Windows PowerShell 路徑中的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 識別碼。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 識別碼可能包含 Windows PowerShell 路徑中不支援的字元。 當您使用 Windows PowerShell 路徑中的識別碼時，必須逸出這些字元或針對這些字元使用特殊編碼。  
  
> [!NOTE]
> 有兩個 SQL Server PowerShell 模組：**SqlServer** 和 **SQLPS**。 **SQLPS** 模組隨附於 SQL Server 安裝 (基於回溯相容性)，但不再更新。 最新版 PowerShell 模組是 **SqlServer** 模組。 **SqlServer** 模組包含 **SQLPS** 中 Cmdlet 的更新版本，此外還加入新的 Cmdlet 以支援最新版 SQL 功能。  
> 舊版 **SqlServer** 模組隨附於 SQL Server Management Studio (SSMS)，但僅限 SSMS 16.x 版。 若要搭配 SSMS 17.0 和更新版本使用 PowerShell，則必須從 PowerShell 資源庫安裝 **SqlServer** 模組。
> 若要安裝 **SqlServer** 模組，請參閱[安裝 SQL Server PowerShell](download-sql-server-ps-module.md)。


## <a name="sql-server-identifiers-in-windows-powershell-paths"></a>Windows PowerShell 路徑中的 SQL Server 識別碼  
 Windows PowerShell 提供者會使用與 Windows 檔案系統類似的路徑結構來公開資料階層。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 提供者會實作 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 物件的路徑。 如果是 [!INCLUDE[ssDE](../includes/ssde-md.md)]，磁碟機會設定為 SQLSERVER:、第一個資料夾會設定為 \SQL，而且資料庫物件會當做容器和項目來參考。 這是預設 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 執行個體中 [!INCLUDE[ssDE](../includes/ssde-md.md)]資料庫之 Purchasing 結構描述的 Vendor 資料表路徑：  
  
```  
SQLSERVER:\SQL\MyComputer\DEFAULT\Databases\AdventureWorks2012\Tables\Purchasing.Vendor  
```  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 識別碼為 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 物件的名稱，例如資料表或資料行名稱。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 識別碼有兩種：  
  
-   一般識別碼限制為 Windows PowerShell 路徑中也支援的一組字元。 這些名稱可以在 Windows PowerShell 路徑中使用，而不需變更。  
  
-   分隔識別碼可以使用 Windows PowerShell 路徑名稱中不支援的字元。 分隔識別碼如果放在括號內 ([IdentifierName])，則稱為括號識別碼，而如果是放在雙引號內 ("IdentifierName")，則稱為引號識別碼。 如果分隔識別碼使用 Windows PowerShell 路徑中不支援的字元，這些字元必須先編碼或逸出，然後才可以使用該識別碼當做容器或項目名稱。 編碼適用於所有字元。 某些字元 (例如冒號字元 (:)) 無法逸出。  
  
## <a name="sql-server-identifiers-in-cmdlets"></a>Cmdlet 中的 SQL Server 識別碼  
 某些 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Cmdlet 有一個參數會將識別碼當做輸入。 參數值通常會以加上引號的字串常數形式提供，或是在字串變數中提供。 當以字串常數的形式或是在變數中提供識別碼時，不會與 Windows PowerShell 支援的字元集合發生衝突。  
  
## <a name="sql-server-identifier-tasks"></a>SQL Server 識別碼工作  
  
|工作描述|發行項|  
|----------------------|-----------|  
|描述如何指定執行個體名稱，包括執行個體在其上執行的電腦名稱。|[指定 SQL Server PowerShell 提供者中的執行個體](specify-instances-in-the-sql-server-powershell-provider.md)|  
|描述如何指定用於 Windows PowerShell 路徑中不支援之分隔識別碼的十六進位編碼。 同時描述如何解碼十六進位字元。|[編碼及解碼 SQL Server 識別碼](encode-and-decode-sql-server-identifiers.md)|  
|描述如何使用 PowerShell 路徑中不支援字元的 Windows PowerShell 逸出字元。|[逸出 SQL Server 識別碼](escape-sql-server-identifiers.md)|  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server PowerShell 提供者](sql-server-powershell-provider.md)   
 [SQL Server PowerShell](sql-server-powershell.md)   
 [資料庫識別碼](../relational-databases/databases/database-identifiers.md)  
  
  
