---
title: 編碼及解碼 SQL Server 識別碼 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: bb9fe0d3-e432-42d3-b324-64dc908b544a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d2acb1b560e6a1399751e263f1437f5da1c85aeb
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2018
ms.locfileid: "52415878"
---
# <a name="encode-and-decode-sql-server-identifiers"></a>編碼及解碼 SQL Server 識別碼
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

SQL Server 分隔識別碼有時會包含 Windows PowerShell 路徑中不支援的字元。 編碼這些字元的十六進位值，就可以指定這些字元。  

> [!NOTE]
> 有兩個 SQL Server PowerShell 模組：**SqlServer** 和 **SQLPS**。 **SQLPS** 模組隨附於 SQL Server 安裝 (基於回溯相容性)，但不再更新。 最新版 PowerShell 模組是 **SqlServer** 模組。 **SqlServer** 模組包含 **SQLPS** 中 Cmdlet 的更新版本，此外還加入新的 Cmdlet 以支援最新版 SQL 功能。  
> 舊版 **SqlServer** 模組隨附於 SQL Server Management Studio (SSMS)，但僅限 SSMS 16.x 版。 若要搭配 SSMS 17.0 和更新版本使用 PowerShell，則必須從 PowerShell 資源庫安裝 **SqlServer** 模組。
> 若要安裝 **SqlServer** 模組，請參閱[安裝 SQL Server PowerShell](download-sql-server-ps-module.md)。
  
  
Windows PowerShell 路徑名稱中不支援的字元可以表示或編碼為 "%" 字元，後面緊接著代表此字元之位元模式的十六進位值，就像是 "**%** xx"。 編碼一定可以用來處理 Windows PowerShell 路徑中不支援的字元。  
  
 **Encode-SqlName** Cmdlet 會將 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 識別碼作為輸入。 它會輸出一個字串，其中包含編碼為 "%xx" 之 Windows PowerShell 語言不支援的所有字元。 **Decode-SqlName** Cmdlet 會將編碼的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 識別碼作為輸入，並傳回原始識別碼。  
  
##  <a name="LimitationsRestrictions"></a> 限制事項  
 **Encode-Sqlname** 和 **Decode-Sqlname** Cmdlet 只能編碼或解碼 SQL Server 分隔識別碼中所允許，但是 PowerShell 路徑中不支援的字元。 下列為 **Encode-SqlName** 所編碼和 **Decode-SqlName** 所解碼的字元：  
  
|||||||||||||  
|-|-|-|-|-|-|-|-|-|-|-|-|  
|**字元**|\|/|所解碼的字元：|%|\<|>|*|?|[|]|&#124;|  
|**十六進位編碼**|%5C|%2F|%3A|%25|%3C|%3E|%2A|%3F|%5B|%5D|%7C|  
  
##  <a name="EncodeIdent"></a> 編碼識別碼  
 **編碼 PowerShell 路徑中的 SQL Server 識別碼**  
  
-   使用兩種方法的其中一種來編碼 SQL Server 識別碼：  
  
    -   使用語法 %XX 指定不支援字元的十六進位代碼，其中 XX 是十六進位代碼。  
  
    -   識別碼會以加上引號的字串形式傳遞給 **Encode-Sqlname** Cmdlet  
  
### <a name="examples-encoding"></a>範例 (編碼)  
 此範例指定 ":" 字元 (%3A) 的編碼版本：  
  
```  
Set-Location Table%3ATest  
```  
  
 您也可以使用 **Encode-SqlName** 來建立 Windows PowerShell 所支援的名稱：  
  
```  
Set-Location (Encode-SqlName "Table:Test")  
```  
  
##  <a name="DecodeIdent"></a> 解碼識別碼  
 **解碼 PowerShell 路徑中的 SQL Server 識別碼**  
  
 **Decode-Sqlname** Cmdlet 可用來將十六進位編碼取代為該編碼所代表的字元。  
  
### <a name="examples-decoding"></a>範例 (解碼)  
 此範例會傳回 "Table:Test"：  
  
```  
Decode-SqlName "Table%3ATest"  
```  
  
## <a name="see-also"></a>另請參閱  
 [PowerShell 中的 SQL Server 識別碼](sql-server-identifiers-in-powershell.md)   
 [SQL Server PowerShell 提供者](sql-server-powershell-provider.md)   
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  
