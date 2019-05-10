---
title: 支援的 SQL Server 2019 SQL 伺服器語言擴充功能的 Java 資料類型
description: 對應的資料類型從 Java 到 SQL Server 針對輸入和輸出資料結構，以及在 sp_execute_external_script 的輸入參數。
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/23/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 14a2bc5594b16610dfb8278ab82a9e7b8b22fea6
ms.sourcegitcommit: d5cd4a5271df96804e9b1a27e440fb6fbfac1220
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/28/2019
ms.locfileid: "64774996"
---
# <a name="java-and-sql-server-supported-data-types"></a>Java 和 SQL Server 支援的資料類型

這篇文章上的對應為 Java 資料類型的資料結構和參數的 SQL Server 資料類型[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)。

## <a name="data-types-for-data-sets"></a>資料集的資料類型

對於輸入和輸出資料集目前支援下列的 SQL 和 Java 資料類型。


| SQL 資料類型        | Java 資料類型 | 註解 | |
| ------------- |-------------|-|-|
| bit      | boolean | | |
| Tinyint      | short      | | |
| Smallint | short      | | |
| int | ssNoversion      | | |
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
| char(n) | String | 只支援 UTF8 字串 | |
| varchar(n) | String | 只支援 UTF8 字串 | |
| varchar(max) | String | 只支援 UTF8 字串 | |

## <a name="data-types-for-input-parameters"></a>輸入參數的資料類型

目前支援下列的 SQL 和 Java 資料類型當做輸入參數。

| SQL 資料類型        | Java 資料類型 | 註解 | |
| ------------- |-------------|-|-|
| bit      | boolean | | |
| Tinyint      | short      | | |
| Smallint | short      | | |
| int | ssNoversion      | | |
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
| char(n) | String | 只支援 UTF8 字串 | |
| varchar(n) | String | 只支援 UTF8 字串 | |
| varchar(max) | String | 只支援 UTF8 字串 | |

## <a name="next-steps"></a>後續步驟

+ [如何在 SQL Server 呼叫 Java](howto-call-java-from-sql.md)
+ [SQL Server 中的 Java 範例](java-first-sample.md)
+ [SQL Server 中的 Java 語言擴充功能](extension-java.md)
