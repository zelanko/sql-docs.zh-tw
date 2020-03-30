---
title: 逸出 SQL Server 識別碼 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: 8a73e945-daa6-4e5d-93da-10f000f1f3a2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c196b316424c941cba52eb50c61c82ca772ba18c
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "67951701"
---
# <a name="escape-sql-server-identifiers"></a>逸出 SQL Server 識別碼
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

您可以經常使用反勾號逸出字元 (`) 來逸出 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 分隔識別碼中所允許，但是 Windows PowerShell 路徑名稱所不允許的字元。 但是，某些字元無法逸出。 例如，您無法逸出 Windows PowerShell 中的冒號字元 (:)。 具有該字元的識別碼必須加以編碼。 編碼比逸出更為可靠，因為編碼適用於所有字元。  

> [!NOTE]
> 有兩個 SQL Server PowerShell 模組：**SqlServer** 和 **SQLPS**。 **SQLPS** 模組隨附於 SQL Server 安裝 (基於回溯相容性)，但不再更新。 最新版 PowerShell 模組是 **SqlServer** 模組。 **SqlServer** 模組包含 **SQLPS** 中 Cmdlet 的更新版本，此外還加入新的 Cmdlet 以支援最新版 SQL 功能。
> 舊版 **SqlServer** 模組隨附於  SQL Server Management Studio (SSMS)，但僅限 SSMS 16.x 版。 若要搭配 SSMS 17.0 和更新版本使用 PowerShell，則必須從 PowerShell 資源庫安裝 **SqlServer** 模組。
> 若要安裝 **SqlServer** 模組，請參閱[安裝 SQL Server PowerShell](download-sql-server-ps-module.md)。

反勾號字元 (`) 通常是在鍵盤左上方 ESC 鍵底下的按鍵上。  
  
## <a name="examples"></a>範例  
 這是逸出 # 字元的範例：  
  
```  
cd SQLSERVER:\SQL\MyComputer\MyInstance\MyDatabase\MySchema\`#MyTempTable  
```  
  
 這是指定 (local) 做為電腦名稱時的逸出括號範例：  
  
```  
Set-Location SQLSERVER:\SQL\`(local`)\DEFAULT  
```  
  
## <a name="see-also"></a>另請參閱  
 [PowerShell 中的 SQL Server 識別碼](sql-server-identifiers-in-powershell.md)   
 [SQL Server PowerShell 提供者](sql-server-powershell-provider.md)   
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  
