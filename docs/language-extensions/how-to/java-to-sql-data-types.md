---
title: Java 資料類型
titleSuffix: SQL Server Language Extensions
description: 將資料類型從 Java 對應至 SQL Server，以供輸入和輸出資料結構以及 sp_execute_external_script 的輸入參數使用。
author: dphansen
ms.author: davidph
ms.date: 11/05/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 26c5e6f344d9fb0a14a21fa195214c4460673de0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85748508"
---
# <a name="java-and-sql-server-supported-data-types"></a>Java 與 SQL Server 支援的資料類型
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

此文章會將 SQL Server 資料類型對應到 Java 資料類型，以供 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) 的資料結構與參數使用。

下列 SQL 與 Java 資料類型目前支援輸入/輸出資料集與輸入/輸出參數。

| SQL 資料類型        | Java 資料類型 | 註解 | |
| ------------- |-------------|-|-|
| bit      | boolean | | |
| Tinyint      | short      | | |
| Smallint | short      | | |
| Int | int      | | |
| Real | FLOAT      | | |
| Bigint | long      | | |
| FLOAT | double      | | |
| nchar(n) | String      | | |
| nvarchar(n) | String      | | |
| binary(n) | byte[]      | | |
| varbinary(n) | byte[]      | | |
| nvarchar(max) | String      | | |
| varbinary(max) | byte[]      | | |
| UNIQUEIDENTIFIER | String | | |
| char(n) | String | 僅支援 UTF8 字串 | |
| varchar(n) | String | 僅支援 UTF8 字串 | |
| varchar(max) | String | 僅支援 UTF8 字串 | |
| date | java.sql.date  | | |
| NUMERIC | java.math.BigDecimal  | | |
| decimal | java.math.BigDecimal  | | |
| money | java.math.BigDecimal  | | |
| SMALLMONEY | java.math.BigDecimal  | | |
| smalldatetime | java.sql.timestamp  | | |
| Datetime | java.sql.timestamp  | | |
| datetime2 | java.sql.timestamp  | | |


## <a name="next-steps"></a>後續步驟

+ [如何在 SQL Server 中呼叫 Java](../how-to/call-java-from-sql.md)
