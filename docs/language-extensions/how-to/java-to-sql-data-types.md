---
title: SQL Server 2019 中支援的 Java 資料類型
titleSuffix: SQL Server Language Extensions
description: 將資料類型從 Java 對應至 SQL Server，以供輸入和輸出資料結構以及 sp_execute_external_script 的輸入參數使用。
author: dphansen
ms.author: davidph
ms.date: 09/05/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9daca9c607befe077fcccec20385a36c82b04c6f
ms.sourcegitcommit: a97d551b252b76a33606348082068ebd6f2c4c8c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/06/2019
ms.locfileid: "73588832"
---
# <a name="java-and-sql-server-supported-data-types"></a>Java 與 SQL Server 支援的資料類型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

此文章會將 SQL Server 資料類型對應到 Java 資料類型，以供 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) 的資料結構與參數使用。

下列 SQL 與 Java 資料類型目前支援輸入/輸出資料集與輸入/輸出參數。

| SQL 資料類型        | Java 資料類型 | 註解 | |
| ------------- |-------------|-|-|
| bit      | boolean | | |
| Tinyint      | short      | | |
| Smallint | short      | | |
| int | INT      | | |
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
| 日期 | java.sql.date  | | |
| NUMERIC | java.math.BigDecimal  | | |
| Decimal | java.math.BigDecimal  | | |
| money | java.math.BigDecimal  | | |
| SMALLMONEY | java.math.BigDecimal  | | |
| smalldatetime | java.sql.timestamp  | | |
| DATETIME | java.sql.timestamp  | | |
| datetime2 | java.sql.timestamp  | | |


## <a name="next-steps"></a>後續步驟

+ [如何在 SQL Server 中呼叫 Java](../how-to/call-java-from-sql.md)
