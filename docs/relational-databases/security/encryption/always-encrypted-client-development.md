---
title: 使用 Always Encrypted 開發應用程式 | Microsoft Docs
description: 了解 Always Encrypted 用戶端加密技術，可確保敏感性資料 (及相關的加密金鑰) 永遠不會洩漏給 SQL Server 或 Azure SQL Database。
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
ms.openlocfilehash: 6f348cf050941a06b2e0be6c37993a7f7458cb6a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85627568"
---
# <a name="develop-applications-using-always-encrypted"></a>使用 Always Encrypted 開發應用程式
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]

[永遠加密](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)是一項用戶端加密技術，可確保敏感性資料 (及相關的加密金鑰) 永遠不會洩漏給 SQL Server 或 Azure SQL Database。 透過永遠加密，用戶端驅動程式可以明確地加密敏感性資料，再將資料傳遞至資料庫引擎，而且可以將擷取自已加密資料庫資料行的資料明確地解密。

如需開發使用受永遠加密保護之資料庫的應用程式，以及哪些用戶端驅動程式和驅動程式版本支援永遠加密的詳細資訊，請參閱：

- [搭配 .NET Framework Data Provider for SQL Server 使用 [永遠加密]](../../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)
- [搭配使用一律加密與 JDBC 驅動程式](../../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)
- [搭配使用 Always Encrypted 與 JDBC 驅動程式](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)
- [搭配使用 Always Encrypted 與 PHP 驅動程式](../../../connect/php/using-always-encrypted-php-drivers.md)
- [在 .NET Core 和 .NET Framework 應用程式中搭配使用 Always Encrypted 與 Microsoft .NET Data Provider for SQL Server](../../../connect/ado-net/sql/sqlclient-support-always-encrypted.md)
- [一律加密](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
