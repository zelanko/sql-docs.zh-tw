---
title: 使用 Azure Active Directory |適用於 SQL Server 的 Microsoft Docs
ms.custom: ''
ms.date: 01/28/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: bazizi
ms.author: v-beaziz
ms.openlocfilehash: 44f92e782a497005ea47847301279e4341722d36
ms.sourcegitcommit: 958cffe9288cfe281280544b763c542ca4025684
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 02/23/2019
ms.locfileid: "56744799"
---
# <a name="using-azure-active-directory"></a>使用 Azure Active Directory
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

## <a name="purpose"></a>目的

從 18.2.1 版開始，Microsoft OLE DB Driver for SQL Server 可讓 OLE DB 應用程式連接到 Azure SQL Database 的執行個體使用同盟身分識別。 新的驗證方法包括：
- Azure Active Directory 登入識別碼和密碼
- Azure Active Directory 存取權杖
- Azure Active Directory 整合式驗證
- SQL 登入識別碼和密碼

> [!NOTE]  
> 使用下列的 Azure Active Directory 選項搭配時，OLE DB 驅動程式，請確認[適用於 SQL Server 的 Active Directory Authentication Library](https://go.microsoft.com/fwlink/?LinkID=513072)已安裝：
> - Azure Active Directory 登入識別碼和密碼
> - Azure Active Directory 整合式驗證
>
> ADAL 不需要其他驗證方法或 OLE DB 作業。

> [!NOTE]
> 使用下列驗證模式與`DataTypeCompatibility`（或其對應的屬性） 設定為`80`是**不**支援：
> - 使用登入識別碼和密碼的 azure Active Directory 驗證
> - 使用存取權杖的 azure Active Directory 驗證
> - Azure Active Directory 整合式驗證

## <a name="connection-string-keywords-and-properties"></a>連接字串關鍵字和屬性
已引進下列連接字串關鍵字來支援 Azure Active Directory 驗證：

|連接字串關鍵字|連線屬性|描述|
|---               |---                |---        |
|存取權杖|SSPROP_AUTH_ACCESS_TOKEN|指定存取權杖來向 Azure Active Directory 進行驗證。 |
|驗證|SSPROP_AUTH_MODE|指定要使用的驗證方法。|

如需新的關鍵字/屬性的詳細資訊，請參閱下列頁面：
- [利用 OLE DB Driver for SQL Server 使用連接字串關鍵字](../applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)
- [初始化和授權屬性](../ole-db-data-source-objects/initialization-and-authorization-properties.md)

## <a name="encryption-and-certificate-validation"></a>加密和憑證驗證
本章節討論中加密和憑證驗證行為的變更。 這些變更將會**只**生效時使用新的驗證或存取權杖連接字串關鍵字 （或其對應的屬性）。

### <a name="encryption"></a>加密
為了提高安全性，使用新連接的屬性/關鍵字時，驅動程式會覆寫預設的加密值設定為`yes`。 覆寫會發生在資料來源物件初始化階段。 加密透過任何方式設定初始化之前，如果的值是遵守，且不會被覆寫。

> [!NOTE]   
> 在 ADO 應用程式和應用程式，取得`IDBInitialize`透過介面`IDataInitialize::GetDataSource`，明確實作介面的核心元件的預設值來設定加密`no`。 如此一來，這項設定及加密值會採用新的驗證屬性/關鍵字**不是**覆寫。 因此，很**建議**明確將這些應用程式設定`Use Encryption for Data=true`覆寫預設值。

### <a name="certificate-validation"></a>憑證驗證
為了提高安全性，採用新的連接屬性/關鍵字`TrustServerCertificate`設定 （和其對應的連接字串關鍵字/屬性）**獨立用戶端加密設定**。 如此一來，就是預設驗證伺服器憑證。

> [!NOTE]   
> 也可以透過控制憑證驗證`Value`欄位`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SNI18.0\GeneralFlags\Flag2`登錄項目。 有效值為 `0` 或 `1`。 OLE DB 驅動程式會選擇登錄之間的連線屬性/關鍵字設定最安全的選項。 也就是驅動程式會驗證伺服器憑證，只要至少一個登錄/連線設定可讓伺服器憑證驗證。

## <a name="gui-additions"></a>GUI 新增項目
驅動程式的圖形化使用者介面已經過增強，以允許 Azure Active Directory 驗證。 如需詳細資訊，請參閱：
- [SQL Server 登入對話方塊](../help-topics/sql-server-login-dialog.md)
- [通用資料連結 (UDL) 設定](../help-topics/data-link-pages.md)

## <a name="example-connection-strings"></a>範例連接字串
此區段會顯示範例的新的和現有的連接字串關鍵字搭配`IDataInitialize::GetDataSource`和`DBPROP_INIT_PROVIDERSTRING`屬性。

### <a name="sql-authentication"></a>SQL 驗證
- 使用 `IDataInitialize::GetDataSource`：
    - 新增：
        > 提供者 = MSOLEDBSQL; 資料來源 = [伺服器]; Initial Catalog = [database];**Authentication = SqlPassword**;使用者識別碼 = [username];密碼 = [password];使用加密資料 = true
    - 已淘汰：
        > 提供者 = MSOLEDBSQL; 資料來源 = [伺服器]; Initial Catalog = [database];使用者識別碼 = [username];密碼 = [password];使用加密資料 = true
- 使用 `DBPROP_INIT_PROVIDERSTRING`：
    - 新增：
        > Server=[server];Database=[database];**Authentication=SqlPassword**;UID=[username];PWD=[password];Encrypt=yes
    - 已淘汰：
        > Server=[server];Database=[database];UID=[username];PWD=[password];Encrypt=yes

### <a name="integrated-windows-authentication-using-security-support-provider-interface--sspi"></a>使用安全性支援提供者介面 (SSPI) 的整合式的 Windows 驗證

- 使用 `IDataInitialize::GetDataSource`：
    - 新增：
        > 提供者 = MSOLEDBSQL; 資料來源 = [伺服器]; Initial Catalog = [database];**Authentication = ActiveDirectoryIntegrated**;使用加密資料 = true
    - 已淘汰：
        > 提供者 = MSOLEDBSQL; 資料來源 = [伺服器]; Initial Catalog = [database];**整合式安全性 = SSPI**;使用加密資料 = true
- 使用 `DBPROP_INIT_PROVIDERSTRING`：
    - 新增：
        > Server=[server];Database=[database];**Authentication=ActiveDirectoryIntegrated**;Encrypt=yes
    - 已淘汰：
        > Server=[server];Database=[database];**Trusted_Connection=yes**;Encrypt=yes

### <a name="aad-username-and-password-authentication-using-adal"></a>使用 ADAL 的 AAD 使用者名稱和密碼驗證

- 使用 `IDataInitialize::GetDataSource`：
    > 提供者 = MSOLEDBSQL; 資料來源 = [伺服器]; Initial Catalog = [database];**Authentication = ActiveDirectoryPassword**;使用者識別碼 = [username];密碼 = [password];使用加密資料 = true
- 使用 `DBPROP_INIT_PROVIDERSTRING`：
    > Server=[server];Database=[database];**Authentication=ActiveDirectoryPassword**;UID=[username];PWD=[password];Encrypt=yes

### <a name="integrated-azure-active-directory-authentication-using-adal"></a>使用 ADAL 的整合式的 Azure Active Directory 驗證

- 使用 `IDataInitialize::GetDataSource`：
    > 提供者 = MSOLEDBSQL; 資料來源 = [伺服器]; Initial Catalog = [database];**Authentication = ActiveDirectoryIntegrated**;使用加密資料 = true
- 使用 `DBPROP_INIT_PROVIDERSTRING`：
    > Server=[server];Database=[database];**Authentication=ActiveDirectoryIntegrated**;Encrypt=yes

### <a name="azure-active-directory-authentication-using-an-access-token"></a>使用存取權杖的 azure Active Directory 驗證

- 使用 `IDataInitialize::GetDataSource`：
    > 提供者 = MSOLEDBSQL; 資料來源 = [伺服器]; Initial Catalog = [database];**存取權杖 = [存取權杖]**;使用加密資料 = true
- 使用 `DBPROP_INIT_PROVIDERSTRING`：
    > 提供的存取權杖，透過`DBPROP_INIT_PROVIDERSTRING`不支援

## <a name="code-samples"></a>程式碼範例

下列範例顯示，才能連接到 Azure Active Directory 與連接關鍵字的程式碼。 

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
- [授權存取 Azure Active Directory web 應用程式使用 OAuth 2.0 程式碼授與流程](https://go.microsoft.com/fwlink/?linkid=2072672)。

- 了解 [Azure Active Directory 驗證](https://go.microsoft.com/fwlink/?linkid=2073783) (到 SQL Server)。

- 設定使用的驅動程式連線[連接字串關鍵字](../applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)OLE DB 驅動程式支援。
