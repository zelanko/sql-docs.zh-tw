---
title: 使用 Azure Active Directory
description: 了解 Microsoft OLE DB Driver for SQL Server 中所提供，可讓使用者連線至 Azure SQL 資料庫的 Azure Active Directory 驗證方法。
ms.custom: ''
ms.date: 09/30/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: bazizi
ms.author: v-beaziz
ms.openlocfilehash: 71f95203e006141649db7b884b56d085f562974b
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/02/2020
ms.locfileid: "96504699"
---
# <a name="using-azure-active-directory"></a>使用 Azure Active Directory
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

## <a name="purpose"></a>目的


從 [18.2.1](../release-notes-for-oledb-driver-for-sql-server.md#1821) 版開始，Microsoft OLE DB Driver for SQL Server 可讓 OLE DB 應用程式使用同盟識別身分，連線到 Azure SQL Database 的執行個體。 新的驗證方法包括：
- Azure Active Directory 登入識別碼和密碼
- Azure Active Directory 存取權杖
- Azure Active Directory 整合式驗證
- SQL 登入識別碼和密碼


[18.3.0](../release-notes-for-oledb-driver-for-sql-server.md#1830) 版增加對下列驗證方法的支援：
- Azure Active Directory 互動式驗證
- Azure Active Directory 受控識別驗證

[18.5.0](../release-notes-for-oledb-driver-for-sql-server.md#1850) 版增加對下列驗證方法的支援：
- Azure Active Directory 服務主體驗證

> [!NOTE]
> **不** 支援在 `DataTypeCompatibility` (或其對應的屬性) 設定為 `80` 的情況下使用下列驗證模式：
> - 使用登入識別碼和密碼進行 Azure Active Directory 驗證
> - 使用存取權杖進行 Azure Active Directory 驗證
> - Azure Active Directory 整合式驗證
> - Azure Active Directory 互動式驗證
> - Azure Active Directory 受控識別驗證
> - Azure Active Directory 服務主體驗證

## <a name="connection-string-keywords-and-properties"></a>連接字串的關鍵字及屬性
已引入下列連接字串關鍵字來支援 Azure Active Directory 驗證：

|連接字串關鍵字|Connection 屬性|描述|
|---               |---                |---        |
|存取權杖|SSPROP_AUTH_ACCESS_TOKEN|指定用來向 Azure Active Directory 進行驗證的存取權杖。 |
|驗證|SSPROP_AUTH_MODE|指定要使用的驗證方法。|

如需有關新關鍵字/屬性的詳細資訊，請參閱下列頁面：
- [利用 OLE DB Driver for SQL Server 使用連接字串關鍵字](../applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)
- [初始化和授權屬性](../ole-db-data-source-objects/initialization-and-authorization-properties.md)

## <a name="encryption-and-certificate-validation"></a>加密和憑證驗證
本節討論加密和憑證驗證行為的變更。 只有在使用新的驗證或存取權杖連接字串關鍵字 (或其對應的屬性) 時，這些變更 **才會** 生效。

### <a name="encryption"></a>加密
為提升安全性，使用新的連接屬性/關鍵字時，驅動程式會將加密值設定為 `yes` 來覆寫預設值。 在資料來源物件初始化時會發生覆寫。 如果在以任何方式初始化之前設定加密，則會遵守且不會覆寫值。

> [!NOTE]   
> 在 ADO 應用程式中，以及在透過 `IDataInitialize::GetDataSource` 取得 `IDBInitialize` 介面的應用程式中，實作介面的核心元件會將加密明確地設定為其 `no` 預設值。 因此，新的驗證屬性/關鍵字會遵守此設定，而加密值 **不會** 遭到覆寫。 因此，**建議** 這些應用程式明確地設定 `Use Encryption for Data=true` 以覆寫預設值。

### <a name="certificate-validation"></a>憑證驗證
為提升安全性，新的連接屬性/關鍵字會遵守 `TrustServerCertificate` 設定 (及其對應的連接字串關鍵字/屬性)，**而不管用戶端加密設定**。 因此，預設會驗證伺服器憑證。

> [!NOTE]   
> 憑證驗證也可以透過 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SNI18.0\GeneralFlags\Flag2` 登錄項目的 `Value` 欄位控制。 有效值為 `0` 或 `1`。 OLE DB 驅動程式會在登錄和連接屬性/關鍵字設定之間選擇最安全的選項。 也就是說，只要至少其中一個登錄/連線設定啟用伺服器憑證驗證，驅動程式就會驗證伺服器憑證。

## <a name="gui-additions"></a>GUI 新增項目
驅動程式圖形化使用者介面已經過增強，可允許 Azure Active Directory 驗證。 如需詳細資訊，請參閱
- [SQL Server 登入對話方塊](../help-topics/sql-server-login-dialog.md)
- [通用資料連結 (UDL) 設定](../help-topics/data-link-pages.md)

## <a name="example-connection-strings"></a>範例連接字串
本節顯示新連接字串關鍵字和現有連接字串關鍵字的範例，以搭配 `IDataInitialize::GetDataSource` 和 `DBPROP_INIT_PROVIDERSTRING` 屬性使用。

### <a name="sql-authentication"></a>SQL 驗證
- 使用 `IDataInitialize::GetDataSource`：
    - 新增：
        > Provider=MSOLEDBSQL;Data Source=[server];Initial Catalog=[database];**Authentication=SqlPassword**;User ID=[username];Password=[password];Use Encryption for Data=true
    - 已淘汰：
        > Provider=MSOLEDBSQL;Data Source=[server];Initial Catalog=[database];User ID=[username];Password=[password];Use Encryption for Data=true
- 使用 `DBPROP_INIT_PROVIDERSTRING`：
    - 新增：
        > Server=[server];Database=[database];**Authentication=SqlPassword**;UID=[username];PWD=[password];Encrypt=yes
    - 已淘汰：
        > Server=[server];Database=[database];UID=[username];PWD=[password];Encrypt=yes

### <a name="integrated-windows-authentication-using-security-support-provider-interface-sspi"></a>使用安全性支援提供者介面 (SSPI) 進行整合式 Windows 驗證

- 使用 `IDataInitialize::GetDataSource`：
    - 新增：
        > Provider=MSOLEDBSQL;Data Source=[server];Initial Catalog=[database];**Authentication=ActiveDirectoryIntegrated**;Use Encryption for Data=true
    - 已淘汰：
        > Provider=MSOLEDBSQL;Data Source=[server];Initial Catalog=[database];**Integrated Security=SSPI**;Use Encryption for Data=true
- 使用 `DBPROP_INIT_PROVIDERSTRING`：
    - 新增：
        > Server=[server];Database=[database];**Authentication=ActiveDirectoryIntegrated**;Encrypt=yes
    - 已淘汰：
        > Server=[server];Database=[database];**Trusted_Connection=yes**;Encrypt=yes

### <a name="azure-active-directory-username-and-password-authentication"></a>Azure Active Directory 使用者名稱與密碼驗證

- 使用 `IDataInitialize::GetDataSource`：
    > Provider=MSOLEDBSQL;Data Source=[server];Initial Catalog=[database];**Authentication=ActiveDirectoryPassword**;User ID=[username];Password=[password];Use Encryption for Data=true
- 使用 `DBPROP_INIT_PROVIDERSTRING`：
    > Server=[server];Database=[database];**Authentication=ActiveDirectoryPassword**;UID=[username];PWD=[password];Encrypt=yes

### <a name="azure-active-directory-integrated-authentication"></a>Azure Active Directory 整合式驗證

- 使用 `IDataInitialize::GetDataSource`：
    > Provider=MSOLEDBSQL;Data Source=[server];Initial Catalog=[database];**Authentication=ActiveDirectoryIntegrated**;Use Encryption for Data=true
- 使用 `DBPROP_INIT_PROVIDERSTRING`：
    > Server=[server];Database=[database];**Authentication=ActiveDirectoryIntegrated**;Encrypt=yes

### <a name="azure-active-directory-authentication-using-an-access-token"></a>使用存取權杖進行 Azure Active Directory 驗證

- 使用 `IDataInitialize::GetDataSource`：
    > Provider=MSOLEDBSQL;Data Source=[server];Initial Catalog=[database];**Access Token=[access token]**;Use Encryption for Data=true
- 使用 `DBPROP_INIT_PROVIDERSTRING`：
    > 不支援透過 `DBPROP_INIT_PROVIDERSTRING` 提供存取權杖

### <a name="azure-active-directory-interactive-authentication"></a>Azure Active Directory 互動式驗證

- 使用 `IDataInitialize::GetDataSource`：
    > Provider=MSOLEDBSQL;Data Source=[server];Initial Catalog=[database];**Authentication=ActiveDirectoryInteractive**;User ID=[username];Use Encryption for Data=true
- 使用 `DBPROP_INIT_PROVIDERSTRING`：
    > Server=[server];Database=[database];**Authentication=ActiveDirectoryInteractive**;UID=[username];Encrypt=yes

### <a name="azure-active-directory-managed-identity-authentication"></a>Azure Active Directory 受控識別驗證

- 使用 `IDataInitialize::GetDataSource`：
    - 使用者指派的受控識別：
        > Provider=MSOLEDBSQL;Data Source=[server];Initial Catalog=[database];**Authentication=ActiveDirectoryMSI**;User ID=[Object ID];Use Encryption for Data=true
    - 系統指派的受控識別：
        > Provider=MSOLEDBSQL;Data Source=[server];Initial Catalog=[database];**Authentication=ActiveDirectoryMSI**;Use Encryption for Data=true
- 使用 `DBPROP_INIT_PROVIDERSTRING`：
    - 使用者指派的受控識別：
        > Server=[server];Database=[database];**Authentication=ActiveDirectoryMSI**;UID=[Object ID];Encrypt=yes
    - 系統指派的受控識別：
        > Server=[server];Database=[database];**Authentication=ActiveDirectoryMSI**;Encrypt=yes

### <a name="azure-active-directory-service-principal-authentication"></a>Azure Active Directory 服務主體驗證

- 使用 `IDataInitialize::GetDataSource`：
    > Provider=MSOLEDBSQL;Data Source=[server];Initial Catalog=[database];**Authentication=ActiveDirectoryServicePrincipal**;User ID=[Application (client) ID];Password=[Application (client) secret];Use Encryption for Data=true
- 使用 `DBPROP_INIT_PROVIDERSTRING`：
    > Server=[server];Database=[database];**Authentication=ActiveDirectoryServicePrincipal**;UID=[Application (client) ID];PWD=[Application (client) secret];Encrypt=yes

## <a name="code-samples"></a>程式碼範例

下列範例顯示使用連接關鍵字連線到 Azure Active Directory 所需的程式碼。 

### <a name="access-token"></a>存取權杖
```cpp
#include <string>
#include <iostream>
#include <msdasc.h>

int main()
{
    wchar_t azureServer[] = L"server";
    wchar_t azureDatabase[] = L"mydatabase";
    wchar_t accessToken[] = L"eyJ0eXAiOi...";
    IDBInitialize *pIDBInitialize = nullptr;
    IDataInitialize* pIDataInitialize = nullptr;
    HRESULT hr = S_OK;

    CoInitialize(nullptr);

    // Construct the connection string.
    std::wstring connString = L"Provider=MSOLEDBSQL;Data Source=" + std::wstring(azureServer) + L";Initial Catalog=" + 
                              std::wstring(azureDatabase) + L";Access Token=" + accessToken + L";Use Encryption for Data=true;";
    hr = CoCreateInstance(CLSID_MSDAINITIALIZE, nullptr, CLSCTX_INPROC_SERVER, 
                          IID_IDataInitialize, reinterpret_cast<LPVOID*>(&pIDataInitialize));
    if (FAILED(hr))
    {
        std::cout << "Failed to create an IDataInitialize instance." << std::endl;
        goto Cleanup;
    }
    hr = pIDataInitialize->GetDataSource(nullptr, CLSCTX_INPROC_SERVER, connString.c_str(), 
                                         IID_IDBInitialize, reinterpret_cast<IUnknown**>(&pIDBInitialize));
    if (FAILED(hr))
    {
        std::cout << "Failed to get data source object." << std::endl;
        goto Cleanup;
    }
    hr = pIDBInitialize->Initialize();
    if (FAILED(hr))
    {
        std::cout << "Failed to establish connection." << std::endl;
        goto Cleanup;
    }

Cleanup:
    if (pIDBInitialize)
    {
        pIDBInitialize->Uninitialize();
        pIDBInitialize->Release();
    }
    if (pIDataInitialize)
    {
        pIDataInitialize->Release();
    }

    CoUninitialize();
}
```
### <a name="active-directory-integrated"></a>Active Directory 整合式
```cpp
#include <string>
#include <iostream>
#include <msdasc.h>

int main()
{
    wchar_t azureServer[] = L"server";
    wchar_t azureDatabase[] = L"mydatabase";
    IDBInitialize *pIDBInitialize = nullptr;
    IDataInitialize* pIDataInitialize = nullptr;
    HRESULT hr = S_OK;

    CoInitialize(nullptr);

    // Construct the connection string.
    std::wstring connString = L"Provider=MSOLEDBSQL;Data Source=" + std::wstring(azureServer) + L";Initial Catalog=" + 
                              std::wstring(azureDatabase) + L";Authentication=ActiveDirectoryIntegrated;Use Encryption for Data=true;";

    hr = CoCreateInstance(CLSID_MSDAINITIALIZE, nullptr, CLSCTX_INPROC_SERVER, 
                          IID_IDataInitialize, reinterpret_cast<LPVOID*>(&pIDataInitialize));
    if (FAILED(hr)) 
    {
        std::cout << "Failed to create an IDataInitialize instance." << std::endl;
        goto Cleanup;
    }
    hr = pIDataInitialize->GetDataSource(nullptr, CLSCTX_INPROC_SERVER, connString.c_str(), 
                                         IID_IDBInitialize, reinterpret_cast<IUnknown**>(&pIDBInitialize));
    if (FAILED(hr))
    {
        std::cout << "Failed to get data source object." << std::endl;
        goto Cleanup;
    }
    hr = pIDBInitialize->Initialize();
    if (FAILED(hr))
    {
        std::cout << "Failed to establish connection." << std::endl;
        goto Cleanup;
    }

Cleanup:
    if (pIDBInitialize)
    {
        pIDBInitialize->Uninitialize();
        pIDBInitialize->Release();
    }
    if (pIDataInitialize)
    {
        pIDataInitialize->Release();
    }

    CoUninitialize();
}
```

## <a name="next-steps"></a>後續步驟
- [使用 OAuth 2.0 程式碼授與流程，授權存取 Azure Active Directory Web 應用程式](/azure/active-directory/azuread-dev/v1-protocols-oauth-code)。

- 了解 [Azure Active Directory 驗證](/azure/azure-sql/database/authentication-aad-overview) (到 SQL Server)。

- 使用 OLE DB 驅動程式支援的[連接字串關鍵字](../applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)，設定驅動程式連接。