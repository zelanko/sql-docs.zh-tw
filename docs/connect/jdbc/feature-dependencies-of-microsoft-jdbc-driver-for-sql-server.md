---
title: Microsoft JDBC Driver for SQL Server 的功能相依性 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 939a8773-2583-49a4-bf00-6b892fbe39dc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7abf0d389217535292260b6a5b055697eb4b19df
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028087"
---
# <a name="feature-dependencies-of-the-microsoft-jdbc-driver-for-sql-server"></a>Microsoft JDBC Driver for SQL Server 的功能相依性

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

本文會列出 Microsoft JDBC Driver for SQL Server 相依的程式庫。 此專案具有下列相依性。

## <a name="compile-time"></a>編譯時間

 - `com.microsoft.azure:azure-keyvault`：適用於 Always Encrypted Azure Key Vault 功能的 Azure Key Vault Provider (選擇性)
 - `com.microsoft.azure:adal4j`：適用於 Azure Active Directory 驗證功能和 Azure Key Vault 功能的適用於 Java 的 Azure Active Directory 程式庫 (選擇性)
 - `com.microsoft.rest:client-runtime`：適用於 Azure Active Directory 驗證功能和 Azure Key Vault 功能的適用於 Java 的 Azure Active Directory 程式庫 (選擇性)
 - `org.antlr:antlr4-runtime`: ANTLR 4 Runtime for useFmtOnly 功能 (選擇性)
 - `org.osgi:org.osgi.core`：適用於 OSGi Framework 支援的 OSGi Core 程式庫。
 - `org.osgi:org.osgi.compendium`：適用於 OSGi Framework 支援的 OSGi Compendium 程式庫。

## <a name="test-time"></a>測試時間

要求上述其中任一個功能的特定專案，需要明確地在其 POM 檔案中宣告個別相依性。

**例如：** 當您使用 Azure Active Directory 驗證功能時，您需要在專案的 POM 檔案中重新宣告 `adal4j` 相依性。 請參閱下列程式碼片段：

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.4.1.jre11</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.6.4</version>
</dependency>

<dependency>
    <groupId>com.microsoft.rest</groupId>
    <artifactId>client-runtime</artifactId>
    <version>1.6.10</version>
</dependency>
```

**例如：** 當您使用 Azure Key Vault 功能時，您需要在專案的 POM 檔案中重新宣告 `azure-keyvault` 相依性和 `adal4j` 相依性。 請參閱下列程式碼片段：

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.4.1.jre11</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.6.4</version>
</dependency>

<dependency>
    <groupId>com.microsoft.rest</groupId>
    <artifactId>client-runtime</artifactId>
    <version>1.6.10</version>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.2.1</version>
</dependency>
```

## <a name="dependency-requirements-for-the-jdbc-driver"></a>JDBC 驅動程式的相依性需求

### <a name="working-with-the-azure-key-vault-provider"></a>使用 Azure Key Vault 提供者：

- JDBC 驅動程式 7.4.1 版 - 相依性版本：Azure-Keyvault (1.2.1 版)、 Adal4j (1.6.4 版)、Client-Runtime-for-AutoRest (1.6.10) 與其相依性 ([範例應用程式](../../connect/jdbc/azure-key-vault-sample-version-7.0.md))
- JDBC 驅動程式 7.2.2 版 - 相依性版本：Azure-Keyvault (1.2.0 版)、Azure-Keyvault-Webkey (1.2.0 版)、 Adal4j (1.6.3 版)、Client-Runtime-for-AutoRest (1.6.5) 與其相依性 ([範例應用程式](../../connect/jdbc/azure-key-vault-sample-version-7.0.md))
- JDBC 驅動程式 7.0.0 版 - 相依性版本：Azure-Keyvault (1.0.0 版)、Adal4j (1.6.0 版) 與其相依性 ([範例應用程式](../../connect/jdbc/azure-key-vault-sample-version-7.0.md))
- JDBC 驅動程式 6.4.0 版 - 相依性版本：Azure-Keyvault (1.0.0 版)、Adal4j (1.4.0 版) 與其相依性 ([範例應用程式](../../connect/jdbc/azure-key-vault-sample-version-6.2.2.md))
- JDBC 驅動程式 6.2.2 版 - 相依性版本：Azure-Keyvault (1.0.0 版 )、Adal4j (1.4.0 版) 與其相依性 ([範例應用程式](../../connect/jdbc/azure-key-vault-sample-version-6.2.2.md))
- JDBC 驅動程式 6.0.0 版 - 相依性版本：Azure-Keyvault (0.9.7 版)、Adal4j (1.3.0 版) 與其相依性 ([範例應用程式](../../connect/jdbc/azure-key-vault-sample-version-6.0.0.md))

> [!NOTE]
> 透過 6.2.2 和 6.4.0 驅動程式版本，已將 azure-keyvault-java 相依性更新為 1.0.0 版。 不過，新版本與先前版本 (0.9.7) 不相容，並且會中斷驅動程式中現有的實作。 驅動程式中的新實作需要 API 變更，接著會中斷使用 Azure Key Vault Provider 的用戶端程式。
>
> 此問題已透過最新的驅動程式版本 (7.0.0 及後續版本) 解決。 使用驗證回呼機制的已移除建構函式會加回 Azure Key Vault Provider，以提供回溯相容性。

### <a name="working-with-azure-active-directory-authentication"></a>使用 Azure Active Directory 驗證：

- JDBC Driver 7.4.1 版 - 相依性版本：Adal4j (1.6.4 版)、Client-Runtime-for-AutoRest (1.6.10) 與其相依性
- JDBC Driver 7.2.2 版 - 相依性版本：Adal4j (1.6.3 版)、Client-Runtime-for-AutoRest (1.6.5) 與其相依性
- JDBC Driver 7.0.0 版 - 相依性版本：Adal4j (1.6.0 版) 與其相依性
- JDBC Driver 6.4.0 版 - 相依性版本：Adal4j (1.4.0 版) 與其相依性
- JDBC Driver 6.2.2 版 - 相依性版本：Adal4j (1.4.0 版) 與其相依性
- JDBC Driver 6.0.0 版 - 相依性版本：Adal4j (1.3.0 版) 與其相依性。 在此版本的驅動程式中，您可以藉由只在 Windows 作業系統上使用 _ActiveDirectoryIntegrated_ 驗證模式，以及使用 sqljdbc_auth.dll 和適用於 SQL Server 的 Active Directory 驗證程式庫 (ADALSQL.DLL) 來連線。

從驅動程式 6.4.0 版開始，應用程式不一定需要在 Windows 作業系統上使用 ADALSQL.DLL。 針對*非 Windows 作業系統*，驅動程式需要 Kerberos 票證，才能使用 ActiveDirectoryIntegrated 驗證。 如需如何使用 Kerberos 連線至 Active Directory 的詳細資訊，請參閱[在 Windows、Linux 和 Mac 上設定 Kerberos 票證](https://docs.microsoft.com/sql/connect/jdbc/connecting-using-azure-active-directory-authentication#set-kerberos-ticket-on-windows-linux-and-mac) \(機器翻譯\)。

針對 *Windows 作業系統*，驅動程式預設會尋找 sqljdbc_auth.dll，而且不需要設定 Kerberos 票證或 Azure 程式庫相依性。 如果 sqljdbc_auth.dll 無法使用，驅動程式就會尋找可用來向 Active Directory 進行驗證的 Kerberos 票證，就像在其他作業系統上一樣。

您可以取得使用此功能的[範例應用程式](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md)。

## <a name="see-also"></a>另請參閱

[JDBC Driver GitHub 存放庫](https://github.com/microsoft/mssql-jdbc) \(英文\)  
[JDBC Driver API 參考](../../connect/jdbc/reference/jdbc-driver-api-reference.md)
