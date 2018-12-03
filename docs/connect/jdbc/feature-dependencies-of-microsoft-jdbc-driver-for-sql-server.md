---
title: Microsoft JDBC Driver for SQL Server 的功能相依性 | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 939a8773-2583-49a4-bf00-6b892fbe39dc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 01388e48e12a01e18b837cac8e663bf2f52ebe40
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52502632"
---
# <a name="feature-dependencies-of-the-microsoft-jdbc-driver-for-sql-server"></a>Microsoft JDBC Driver for SQL Server 的功能相依性。

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

本文列出 Microsoft JDBC Driver for SQL Server 取決於程式庫。 專案會有下列的相依性。

## <a name="compile-time"></a>編譯時間

- `azure-keyvault`： 永遠加密 Azure Key Vault 功能 （選擇性） azure 金鑰保存庫提供者
- `adal4j`： 適用於 Java 的 Azure Active Directory 驗證功能和 Azure Key Vault 功能 （選擇性） azure Active Directory 程式庫

## <a name="test-time"></a>測試時間

需要其中一個上述功能的特定專案，就需要明確宣告在它們的 POM 檔案中的個別相依性。

**例如：** 當您使用 Azure Active Directory 驗證功能時，您需要重新宣告`adal4j`在專案的 POM 檔案中的相依性。 下列程式碼片段，請參閱：

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.0.0.jre10</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.6.0</version>
</dependency>
```

**例如：** 當您使用 Azure Key Vault 功能時，您需要重新宣告`azure-keyvault`相依性和`adal4j`在專案的 POM 檔案中的相依性。 下列程式碼片段，請參閱：

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.0.0.jre10</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.6.0</version>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.0.0</version>
</dependency>
```

## <a name="dependency-requirements-for-the-jdbc-driver"></a>JDBC Driver 的相依性需求

### <a name="working-with-the-azure-key-vault-provider"></a>使用 Azure Key Vault 提供者：

- JDBC 驅動程式版本 7.0.0-相依性版本： Azure key Vault （1.0.0 版）、 Adal4j （1.6.0 版），及其相依性 ([範例應用程式](../../connect/jdbc/azure-key-vault-sample-version-7-0-0.md))
- JDBC 驅動程式版本 6.4.0-相依性版本： Azure key Vault （1.0.0 版）、 Adal4j （1.4.0 版），及其相依性 ([範例應用程式](../../connect/jdbc/azure-key-vault-sample-version-6.2.2.md))
- JDBC 驅動程式版本 6.2.2-相依性版本： Azure key Vault （1.0.0 版）、 Adal4j （1.4.0 版），及其相依性 ([範例應用程式](../../connect/jdbc/azure-key-vault-sample-version-6.2.2.md))
- JDBC 驅動程式版本 6.0.0-相依性版本： Azure key Vault （0.9.7 版）、 Adal4j （1.3.0 版），及其相依性 ([範例應用程式](../../connect/jdbc/azure-key-vault-sample-version-6.0.0.md))

> [!NOTE]
> 6.2.2 和 6.4.0 驅動程式版本已更新 azure 金鑰保存庫 java 相依性版本 1.0.0。 不過，新的版本與先前的版本 (0.9.7) 不相容，而且在驅動程式會中斷現有的實作。 驅動程式中的新實作所需 API 變更，這接著會使用 「 Azure 金鑰保存庫提供者的用戶端程式中斷。
>
> 此問題已解決與最新的驅動程式版本 (7.0.0) 項目。 移除建構函式使用的驗證回呼機制會加回至 Azure 金鑰保存庫提供者，為了與舊版相容。

### <a name="working-with-azure-active-directory-authentication"></a>使用 Azure Active Directory 驗證：

- JDBC 驅動程式版本 7.0.0-相依性版本： Ada4j （1.6.0 版） 和其相依性
- JDBC 驅動程式版本 6.4.0-相依性版本： Adal4j （1.4.0 版） 和其相依性
- JDBC 驅動程式版本 6.2.2-相依性版本： Adal4j （1.4.0 版） 和其相依性
- JDBC 驅動程式版本 6.0.0-相依性版本： Adal4j （1.3.0 版），和其相依性。 在此版本的驅動程式中，您可以藉由連線_ActiveDirectoryIntegrated_驗證模式，只在 Windows 作業系統上，並使用 SQL Server （sqljdbc_auth.dll 和 Active Directory Authentication LibraryADALSQL。DLL)。

從 驅動程式版本 6.4.0 之後，應用程式不一定需要使用 ADALSQL。在 Windows 作業系統上的 DLL。 針對*非 Windows 作業系統*，驅動程式需要使用 ActiveDirectoryIntegrated 驗證的 Kerberos 票證。 如需如何連線至 Active Directory 中，使用 Kerberos 的詳細資訊，請參閱[在 Windows、 Linux 和 Mac 上的設定 Kerberos 票證](https://docs.microsoft.com/sql/connect/jdbc/connecting-using-azure-active-directory-authentication#set-kerberos-ticket-on-windows-linux-and-mac)。

針對*Windows 作業系統*，驅動程式預設會尋找 sqljdbc_auth.dll，而不需要 Kerberos 票證的安裝程式或 Azure 程式庫相依性。 如果 sqljdbc_auth.dll 無法使用，此驅動程式會尋找在其他作業系統上做為 Active Directory 進行驗證的 Kerberos 票證。

您可以取得[範例應用程式](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md)使用這項功能。

## <a name="see-also"></a>另請參閱

[JDBC 驅動程式的 GitHub 存放庫](https://github.com/microsoft/mssql-jdbc)  
 [JDBC 驅動程式 API 參考](../../connect/jdbc/reference/jdbc-driver-api-reference.md)
