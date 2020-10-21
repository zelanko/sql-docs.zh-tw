---
title: 逸出 SQL Server 識別碼
description: SQL Server 分隔識別碼有時會包含 Windows PowerShell 路徑不支援的字元。 了解如何使用反勾號字元來逸出其中一些識別碼。
ms.prod: sql
ms.technology: sql-server-powershell
ms.topic: conceptual
ms.assetid: 8a73e945-daa6-4e5d-93da-10f000f1f3a2
author: markingmyname
ms.author: maghan
ms.reviewer: matteot, drskwier
ms.custom: ''
ms.date: 10/14/2020
ms.openlocfilehash: 4ad4bdc7720d0c405e3982b6b4533b55c2756490
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2020
ms.locfileid: "92005493"
---
# <a name="escape-sql-server-identifiers"></a>逸出 SQL Server 識別碼

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

您可以經常使用反勾號逸出字元 (`) 來逸出 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 分隔識別碼中所允許，但是 Windows PowerShell 路徑名稱所不允許的字元。 但是，某些字元無法逸出。 例如，您無法在 Windows PowerShell 中逸出冒號字元 (:)。 具有該字元的識別碼必須加以編碼。 編碼比逸出更為可靠，因為編碼適用於所有字元。  

[!INCLUDE [sql-server-powershell-version](../includes/sql-server-powershell-version.md)]

反勾號字元 (`) 通常是在鍵盤左上方 ESC 鍵底下的按鍵上。  

## <a name="examples"></a>範例

這是逸出 # 字元的範例：  

```powershell
cd SQLSERVER:\SQL\MyComputer\MyInstance\MyDatabase\MySchema\`#MyTempTable  
```

這是指定 (local) 做為電腦名稱時的逸出括號範例：  

```powershell
Set-Location SQLSERVER:\SQL\`(local`)\DEFAULT  
```

## <a name="see-also"></a>另請參閱

- [PowerShell 中的 SQL Server 識別碼](sql-server-identifiers-in-powershell.md)
- [SQL Server PowerShell 提供者](sql-server-powershell-provider.md)
- [SQL Server PowerShell](sql-server-powershell.md)