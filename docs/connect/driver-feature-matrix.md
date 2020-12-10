---
title: 驅動程式功能支援矩陣
description: 了解 SQL Server 驅動程式支援哪些熱門功能，以及要在何處尋找其相關資訊。
ms.custom: ''
ms.date: 12/03/2020
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-daenge
ms.openlocfilehash: 4fff9c04098bd0796f714d160864e4edb93613ac
ms.sourcegitcommit: 28fecbf61ae7b53405ca378e2f5f90badb1a296a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/04/2020
ms.locfileid: "96595229"
---
# <a name="driver-feature-support-matrix-for-microsoft-sql-server"></a>Microsoft SQL Server 的驅動程式功能支援矩陣

如果打算使用 Microsoft SQL Server 中的功能，該功能可能無法在所有驅動程式中使用。 功能可能不在特定驅動程式中的某些原因包括：

- 此功能不適用於驅動程式技術。
- 這項功能是新功能，尚未在所有驅動程式中實作。
- 特定驅動程式中不需要此功能。
- 會先實作其他功能。

我們希望所有驅動程式都支援每項功能，並努力確保驅動程式之間的功能同位。 不過，這不一定可行。 為了協助根據需求選擇適當的驅動程式，以下清單列出熱門功能和實作這些功能的驅動程式。

- [.NET](#table1)
- [ODBC](#table2)
- [OLE DB](#table2)
- [JDBC](#table2)
- [PHP](#table3)
- [Node.js / JavaScript](#table3)
- [Python](#table3)

| <a id="table1"></a>功能 | [Microsoft.<wbr>Data.<wbr>SqlClient (.NET Core)](ado-net/microsoft-ado-net-sql-server.md) | [Microsoft.<wbr>Data.<wbr>SqlClient (.NET Framework)](ado-net/microsoft-ado-net-sql-server.md) | System.<wbr>Data.<wbr>SqlClient (.NET Core) | [System.<wbr>Data.<wbr>SqlClient (.NET Framework)](/dotnet/framework/data/adonet/sql/) |
| :-- | :-- | :-- | :-- | :-- |
| [一律加密](../relational-databases/security/encryption/always-encrypted-database-engine.md) | [是](ado-net/sql/sqlclient-support-always-encrypted.md) | [是](ado-net/sql/sqlclient-support-always-encrypted.md) | | [是](ado-net/sql/sqlclient-support-always-encrypted.md) |
| [具有安全記憶體保護區的 Always Encrypted](../relational-databases/security/encryption/always-encrypted-enclaves.md) | [是](ado-net/sql/sqlclient-support-always-encrypted.md#enabling-always-encrypted-with-secure-enclaves) | [是](ado-net/sql/sqlclient-support-always-encrypted.md#enabling-always-encrypted-with-secure-enclaves) | | [是](ado-net/sql/sqlclient-support-always-encrypted.md#enabling-always-encrypted-with-secure-enclaves) |
| [Azure Active Directory 存取權杖驗證](/azure/active-directory/develop/access-tokens) | [是](/dotnet/api/system.data.sqlclient.sqlconnection.accesstoken) | [是](/dotnet/api/microsoft.data.sqlclient.sqlconnection.accesstoken) | [是](/dotnet/api/microsoft.data.sqlclient.sqlconnection.accesstoken) | [是](/dotnet/api/microsoft.data.sqlclient.sqlconnection.accesstoken) |
| [Azure Active Directory 密碼驗證](/azure/sql-database/sql-database-aad-authentication) | [是](ado-net/sql/azure-active-directory-authentication.md) | [是](ado-net/sql/azure-active-directory-authentication.md) | | 是 |
| [Azure Active Directory 整合式驗證](/azure/sql-database/sql-database-aad-authentication) | [是](ado-net/sql/azure-active-directory-authentication.md) | [是](ado-net/sql/azure-active-directory-authentication.md) | | 是 |
| [Azure Active Directory 互動式 (MFA) 驗證](/azure/sql-database/sql-database-aad-authentication) | [是](ado-net/sql/azure-active-directory-authentication.md) | [是](ado-net/sql/azure-active-directory-authentication.md) | | 是 |
| [Azure Active Directory 受控識別驗證](/azure/active-directory/managed-identities-azure-resources/overview) | [是](ado-net/sql/azure-active-directory-authentication.md) | [是](ado-net/sql/azure-active-directory-authentication.md) | | |
| [Azure Active Directory 服務主體驗證](/azure/active-directory/develop/app-objects-and-service-principals) | [是](ado-net/sql/azure-active-directory-authentication.md) | [是](ado-net/sql/azure-active-directory-authentication.md) | | |
| [Windows 整合式驗證](/windows-server/security/windows-authentication/windows-authentication-overview) | [是](ado-net/sql/authentication-sql-server.md) | [是](ado-net/sql/authentication-sql-server.md) | [是](/dotnet/framework/data/adonet/sql/authentication-in-sql-server) | [是](/dotnet/framework/data/adonet/sql/authentication-in-sql-server) |
| [大量複製](../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md) | [是](ado-net/sql/bulk-copy-operations-sql-server.md) | [是](ado-net/sql/bulk-copy-operations-sql-server.md) | [是](/dotnet/framework/data/adonet/sql/bulk-copy-operations-in-sql-server) | [是](/dotnet/framework/data/adonet/sql/bulk-copy-operations-in-sql-server) |
| [資料敏感度與分類中繼資料](../relational-databases/security/sql-data-discovery-and-classification.md) | [是](ado-net/sql/data-classification.md) | [是](ado-net/sql/data-classification.md) | 是 | 是 |
| [Multiple Active Result Set (MARS)](../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md) | [是](ado-net/sql/multiple-active-result-sets-mars.md) | [是](ado-net/sql/multiple-active-result-sets-mars.md) | [是](/dotnet/framework/data/adonet/sql/multiple-active-result-sets-mars) | [是](/dotnet/framework/data/adonet/sql/multiple-active-result-sets-mars) |
| [空間資料類型](../relational-databases/spatial/spatial-data-sql-server.md) | | 是 | | 是 |
| [資料表值參數 (TVP)](../relational-databases/tables/use-table-valued-parameters-database-engine.md) | [是](ado-net/sql/table-valued-parameters.md) | [是](ado-net/sql/table-valued-parameters.md) | [是](/dotnet/framework/data/adonet/sql/table-valued-parameters) | [是](/dotnet/framework/data/adonet/sql/table-valued-parameters) |
| [MultiSubnetFailover](../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) | [是](ado-net/sql/sqlclient-support-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) | [是](ado-net/sql/sqlclient-support-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) | [是](/dotnet/api/system.data.sqlclient.sqlconnectionstringbuilder.multisubnetfailover?view=netcore-1.0&preserve-view=true) | [是](/dotnet/api/system.data.sqlclient.sqlconnectionstringbuilder.multisubnetfailover?view=netframework-4.8&preserve-view=true) |
| [透明網路 IP 解析](odbc/using-transparent-network-ip-resolution.md) | | [是](/dotnet/api/microsoft.data.sqlclient.sqlconnection.connectionstring?view=sqlclient-dotnet-1.1&preserve-view=true) | | [是](/dotnet/api/system.data.sqlclient.sqlconnection.connectionstring?view=netframework-4.8&preserve-view=true) |
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

| <a id="table2"></a>功能 | [Windows 上的 ODBC Driver for SQL Server](odbc/microsoft-odbc-driver-for-sql-server.md) | [Linux 和 macOS 上的 ODBC Driver for SQL Server](odbc/microsoft-odbc-driver-for-sql-server.md) | [JDBC Driver for SQL Server](jdbc/microsoft-jdbc-driver-for-sql-server.md) | [OLE DB Driver for SQL Server](oledb/oledb-driver-for-sql-server.md) |
| :-- | :-- | :-- | :-- | :-- |
| [一律加密](../relational-databases/security/encryption/always-encrypted-database-engine.md) | [是](odbc/using-always-encrypted-with-the-odbc-driver.md) | [是](odbc/using-always-encrypted-with-the-odbc-driver.md) | [是](jdbc/using-always-encrypted-with-the-jdbc-driver.md) |
| [具有安全記憶體保護區的 Always Encrypted](../relational-databases/security/encryption/always-encrypted-enclaves.md) | [是](odbc/using-always-encrypted-with-the-odbc-driver.md#enabling-always-encrypted-with-secure-enclaves) | [是](odbc/using-always-encrypted-with-the-odbc-driver.md#enabling-always-encrypted-with-secure-enclaves) | [是](jdbc/using-always-encrypted-with-the-jdbc-driver.md) | |
| [Azure Active Directory 存取權杖驗證](/azure/active-directory/develop/access-tokens) | [是](odbc/using-azure-active-directory.md#authenticating-with-an-access-token) | [是](odbc/using-azure-active-directory.md#authenticating-with-an-access-token) | [是](jdbc/connecting-using-azure-active-directory-authentication.md#connecting-using-access-token) | [是](oledb/features/using-azure-active-directory.md) |
| [Azure Active Directory 密碼驗證](/azure/sql-database/sql-database-aad-authentication) |  [是](odbc/using-azure-active-directory.md) | [是](odbc/using-azure-active-directory.md) | [是](jdbc/connecting-using-azure-active-directory-authentication.md) | [是](oledb/features/using-azure-active-directory.md) |
| [Azure Active Directory 整合式驗證](/azure/sql-database/sql-database-aad-authentication) | [是](odbc/using-azure-active-directory.md) | [是](odbc/using-azure-active-directory.md) | [是](jdbc/connecting-using-azure-active-directory-authentication.md) | [是](oledb/features/using-azure-active-directory.md) |
| [Azure Active Directory 互動式 (MFA) 驗證](/azure/sql-database/sql-database-aad-authentication) | [是](odbc/using-azure-active-directory.md) | | | [是](oledb/features/using-azure-active-directory.md) |
| [Azure Active Directory 受控識別驗證](/azure/active-directory/managed-identities-azure-resources/overview) | [是](odbc/using-azure-active-directory.md) | [是](odbc/using-azure-active-directory.md) | [是](jdbc/connecting-using-azure-active-directory-authentication.md) | [是](oledb/features/using-azure-active-directory.md) |
| [Azure Active Directory 服務主體驗證](/azure/active-directory/develop/app-objects-and-service-principals) | | | | [是](oledb/features/using-azure-active-directory.md) |
| [Windows 整合式驗證](/windows-server/security/windows-authentication/windows-authentication-overview) | 是 | [是](odbc/linux-mac/using-integrated-authentication.md) | [是](jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md) | 是 |
| [大量複製](../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md) | [是](../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md) | [是](../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md) | [是](jdbc/using-bulk-copy-with-the-jdbc-driver.md) | [是](oledb/features/performing-bulk-copy-operations.md) |
| [資料探索與分類中繼資料](../relational-databases/security/sql-data-discovery-and-classification.md) | [是](odbc/data-classification.md) | [是](odbc/data-classification.md) | [是](jdbc/data-discovery-classification-sample.md) | |
| [Multiple Active Result Set (MARS)](../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md) | [是](../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md) | [是](../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md) | | [是](oledb/features/using-multiple-active-result-sets-mars.md) |
| [空間資料類型](../relational-databases/spatial/spatial-data-sql-server.md) | | | [是](jdbc/use-spatial-datatypes.md) | |
| [資料表值參數 (TVP)](../relational-databases/tables/use-table-valued-parameters-database-engine.md) | [是](../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md) | [是](../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md) | [是](jdbc/using-table-valued-parameters.md) | [是](oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md) |
| [MultiSubnetFailover](../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) | [是](../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) | [是](../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) | [是](jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md) | [是](oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) |
| [透明網路 IP 解析](odbc/using-transparent-network-ip-resolution.md) | [是](odbc/using-transparent-network-ip-resolution.md) | [是](odbc/using-transparent-network-ip-resolution.md) | [是](jdbc/setting-the-connection-properties.md) | [是](oledb/features/using-transparent-network-ip-resolution.md) |
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

| <a id="table3"></a>功能 | [Windows 上的 Drivers for PHP for SQL Server](php/microsoft-php-driver-for-sql-server.md)<sup>[1](#note1)</sup> | [Linux 和 macOS 上的 Drivers for PHP for SQL Server](php/microsoft-php-driver-for-sql-server.md)<sup>[1](#note1)</sup> | [Tedious (Node.js)](node-js/node-js-driver-for-sql-server.md) | [pyODBC (Python)](python/pyodbc/python-sql-driver-pyodbc.md)<sup>[1](#note1)</sup> |
| :-- | :-- | :-- | :-- | :-- |
| [一律加密](../relational-databases/security/encryption/always-encrypted-database-engine.md) | [是](php/using-always-encrypted-php-drivers.md) | [是](php/using-always-encrypted-php-drivers.md) | | 是 |
| [具有安全記憶體保護區的 Always Encrypted](../relational-databases/security/encryption/always-encrypted-enclaves.md) | [是](php/always-encrypted-secure-enclaves.md) | [是](php/always-encrypted-secure-enclaves.md) | | 是 |
| [Azure Active Directory 存取權杖驗證](/azure/active-directory/develop/access-tokens) | [是](php/azure-active-directory.md) | [是](php/azure-active-directory.md) | [是](https://tediousjs.github.io/tedious/api-connection.html#function_newConnection) | 是 |
| [Azure Active Directory 密碼驗證](/azure/sql-database/sql-database-aad-authentication) | [是](php/azure-active-directory.md) | [是](php/azure-active-directory.md) | [是](https://tediousjs.github.io/tedious/api-connection.html#function_newConnection) | 是 |
| [Azure Active Directory 整合式驗證](/azure/sql-database/sql-database-aad-authentication) | [是](php/azure-active-directory.md) | [是](php/azure-active-directory.md) | | 是 |
| [Azure Active Directory 互動式 (MFA) 驗證](/azure/sql-database/sql-database-aad-authentication) | | | | 是<sup>[2](#note2)</sup> |
| [Azure Active Directory 受控識別驗證](/azure/active-directory/managed-identities-azure-resources/overview) | [是](php/azure-active-directory.md) | [是](php/azure-active-directory.md) | [是](https://tediousjs.github.io/tedious/api-connection.html#function_newConnection) | 是 |
| [Azure Active Directory 服務主體驗證](/azure/active-directory/develop/app-objects-and-service-principals) | | | | |
| [Windows 整合式驗證](/windows-server/security/windows-authentication/windows-authentication-overview) | [是](php/how-to-connect-using-windows-authentication.md) | [是](odbc/linux-mac/using-integrated-authentication.md) | | 是 |
| [大量複製](../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md) | | | [是](https://tediousjs.github.io/tedious/bulk-load.html) | |
| [資料探索與分類中繼資料](../relational-databases/security/sql-data-discovery-and-classification.md) | 是 | 是 | | |
| [Multiple Active Result Set (MARS)](../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md) | [是](php/how-to-disable-multiple-active-resultsets-mars.md) | [是](php/how-to-disable-multiple-active-resultsets-mars.md) | | 是 |
| [空間資料類型](../relational-databases/spatial/spatial-data-sql-server.md) | | | | |
| [資料表值參數 (TVP)](../relational-databases/tables/use-table-valued-parameters-database-engine.md) | | | [是](https://tediousjs.github.io/tedious/parameters.html) | 是 |
| [MultiSubnetFailover](../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) | [是](php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md) | [是](php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md) | | [是](../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) |
| [透明網路 IP 解析](odbc/using-transparent-network-ip-resolution.md) | [是](php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md) | [是](php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md) | | [是](odbc/using-transparent-network-ip-resolution.md) |
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

<a id="note1"></a><sup>1</sup> 由於這些驅動程式依賴 Microsoft ODBC Driver for SQL Server，因此還必須使用支援該功能的驅動程式版本。

<a id="note2"></a><sup>2</sup> 僅限在 Windows 上。

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
