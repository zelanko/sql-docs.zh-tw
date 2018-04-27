---
title: 逸出 SQL Server 識別碼 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: powershell
ms.service: ''
ms.component: powershell
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8a73e945-daa6-4e5d-93da-10f000f1f3a2
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dda716b6d61a9ec54a61b5a910407810fffd12d5
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="escape-sql-server-identifiers"></a>逸出 SQL Server 識別碼
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

您可以經常使用反勾號逸出字元 (`) 來逸出 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 分隔識別碼中所允許，但是 Windows PowerShell 路徑名稱所不允許的字元。 但是，某些字元無法逸出。 例如，您無法逸出 Windows PowerShell 中的冒號字元 (:)。 具有該字元的識別碼必須加以編碼。 編碼比逸出更為可靠，因為編碼適用於所有字元。  

> [!NOTE]
> 有兩個 SQL Server PowerShell 模組：**SqlServer** 和 **SQLPS**。 **SQLPS** 模組隨附於 SQL Server 安裝 (基於回溯相容性)，但不再更新。 最新版 PowerShell 模組是 **SqlServer** 模組。 **SqlServer** 模組包含 **SQLPS** 中 Cmdlet 的更新版本，此外還加入新的 Cmdlet 以支援最新版 SQL 功能。
> 舊版 **SqlServer** 模組隨附於 SQL Server Management Studio (SSMS)，但僅限 SSMS 16.x 版。 若要搭配 SSMS 17.0 和更新版本使用 PowerShell，則必須從 PowerShell 資源庫安裝 **SqlServer** 模組。
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
  
  
