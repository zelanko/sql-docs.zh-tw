---
title: 編碼及解碼 SQL Server 識別碼
description: SQL Server 分隔識別碼中有時會包含 Windows PowerShell 路徑中不支援的字元。 了解如何使用這些字元的十六進位值呈現字元，以納入這些字元。
ms.prod: sql
ms.technology: sql-server-powershell
ms.topic: conceptual
ms.assetid: bb9fe0d3-e432-42d3-b324-64dc908b544a
author: markingmyname
ms.author: maghan
ms.reviewer: matteot, drskwier
ms.custom: ''
ms.date: 10/14/2020
ms.openlocfilehash: a3f2ab659d77e1b06cb69905971d3954e2eb76da
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2020
ms.locfileid: "92005465"
---
# <a name="encode-and-decode-sql-server-identifiers"></a>編碼及解碼 SQL Server 識別碼

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

SQL Server 分隔識別碼有時會包含 Windows PowerShell 路徑中不支援的字元。 編碼這些字元的十六進位值，就可以指定這些字元。

[!INCLUDE [sql-server-powershell-version](../includes/sql-server-powershell-version.md)]

Windows PowerShell 路徑名稱中不支援的字元可以表示或編碼為 "%" 字元，後面緊接著代表此字元之位元模式的十六進位值，就像是 " **%** xx"。 編碼一定可以用來處理 Windows PowerShell 路徑中不支援的字元。

**Encode-SqlName** Cmdlet 會將 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 識別碼作為輸入。 它會輸出一個字串，其中包含編碼為 "%xx" 之 Windows PowerShell 語言不支援的所有字元。 **Decode-SqlName** Cmdlet 會將編碼的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 識別碼作為輸入，並傳回原始識別碼。  

## <a name="limitations-and-restrictions"></a>限制事項

**Encode-Sqlname** 和 **Decode-Sqlname** Cmdlet 只能編碼或解碼 SQL Server 分隔識別碼中所允許，但是 PowerShell 路徑中不支援的字元。 下列為 **Encode-SqlName** 所編碼和 **Decode-SqlName** 所解碼的字元：

|||||||||||||
|-|-|-|-|-|-|-|-|-|-|-|-|
|**字元**|\ |/|:|%|\<|>|*|?|[|]|&#124;|  
|**十六進位編碼**|%5C|%2F|%3A|%25|%3C|%3E|%2A|%3F|%5B|%5D|%7C|

## <a name="encoding-an-identifier"></a>編碼識別碼  

### <a name="to-encode-a-sql-server-identifier-in-a-powershell-path"></a>編碼 PowerShell 路徑中的 SQL Server 識別碼

- 使用兩種方法的其中一種來編碼 SQL Server 識別碼：
    - 使用語法 %XX 指定不支援字元的十六進位代碼，其中 XX 是十六進位代碼。
    - 識別碼會以加上引號的字串形式傳遞給 **Encode-Sqlname** Cmdlet

### <a name="examples-encoding"></a>範例 (編碼)

此範例指定 ":" 字元 (%3A) 的編碼版本：

```powershell
Set-Location Table%3ATest
```

您也可以使用 **Encode-SqlName** 來建立 Windows PowerShell 所支援的名稱：

```powershell
Set-Location (Encode-SqlName "Table:Test")
```

## <a name="decoding-an-identifier"></a>解碼識別碼

### <a name="to-decode-a-sql-server-identifier-from-a-powershell-path"></a>解碼 PowerShell 路徑中的 SQL Server 識別碼

**Decode-Sqlname** Cmdlet 可用來將十六進位編碼取代為該編碼所代表的字元。

### <a name="examples-decoding"></a>範例 (解碼)

此範例會傳回 "Table:Test"：

```powershell
Decode-SqlName "Table%3ATest"
```

## <a name="see-also"></a>另請參閱

- [PowerShell 中的 SQL Server 識別碼](sql-server-identifiers-in-powershell.md)
- [SQL Server PowerShell 提供者](sql-server-powershell-provider.md)
- [SQL Server PowerShell](sql-server-powershell.md)  
