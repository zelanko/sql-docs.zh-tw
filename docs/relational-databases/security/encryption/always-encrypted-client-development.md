---
title: 使用 Always Encrypted 開發應用程式 | Microsoft Docs
ms.custom: ''
ms.date: 10/30/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
dev_langs:
- CSharp
ms.assetid: 9595eb66-284c-4474-828f-8961a05ce989
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 235dc20ca94affa5f022bc242aa0ef6726f1542c
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/05/2019
ms.locfileid: "73594440"
---
# <a name="develop-applications-using-always-encrypted"></a>使用 Always Encrypted 開發應用程式
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

[永遠加密](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)是一項用戶端加密技術，可確保敏感性資料 (及相關的加密金鑰) 永遠不會洩漏給 SQL Server 或 Azure SQL Database。 透過永遠加密，用戶端驅動程式可以明確地加密敏感性資料，再將資料傳遞至資料庫引擎，而且可以將擷取自已加密資料庫資料行的資料明確地解密。

如需開發使用受永遠加密保護之資料庫的應用程式，以及哪些用戶端驅動程式和驅動程式版本支援永遠加密的詳細資訊，請參閱：

- [搭配 .NET Framework Data Provider for SQL Server 使用 [永遠加密]](../../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)
- [搭配使用一律加密與 JDBC 驅動程式](../../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)
- [搭配使用 Always Encrypted 與 JDBC 驅動程式](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)
- [搭配使用 Always Encrypted 與 PHP 驅動程式](../../../connect/php/using-always-encrypted-php-drivers.md)
- [使用 Always Encrypted .NET Core 和 .NET Framework 應用程式中的 Microsoft.Data.SqlClient](https://github.com/dotnet/sqlclient/tree/master/release-notes)
- [永遠加密](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
