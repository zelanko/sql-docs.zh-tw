---
title: 搭配 SqlClient 使用 Azure Active Directory 驗證
description: 說明如何使用支援的 Azure Active Directory 驗證模式，透過 SqlClient 連線到 Azure SQL 資料來源
ms.date: 11/20/2020
dev_langs:
- csharp
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: karinazhou
ms.author: v-jizho2
ms.reviewer: ''
ms.openlocfilehash: 0f8aaffc1f87b33a5c685b55d724fe96c44258af
ms.sourcegitcommit: ece151df14dc2610d96cd0d40b370a4653796d74
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96297945"
---
# <a name="using-azure-active-directory-authentication-with-sqlclient"></a>搭配 SqlClient 使用 Azure Active Directory 驗證

[!INCLUDE [appliesto-netfx-netcore-netst-md](../../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE [Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

此文章說明如何從 .NET 應用程式，搭配 SqlClient 使用 Azure Active Directory (Azure AD) 驗證來連線到 Azure SQL 資料來源。

Azure AD 驗證會使用 Azure AD 中的身分識別來存取 Azure SQL 資料來源，例如，Azure SQL Database、Azure SQL 受控執行個體與 Azure Synapse Analytics。 **Microsoft.Data.SqlClient** 命名空間可讓用戶端應用程式在連線到 Azure SQL Database 時，以不同的驗證模式指定 Azure AD 認證。 

當您在連接字串中設定 `Authentication` 連線屬性時，用戶端可以根據提供的值選擇慣用的 Azure AD 驗證模式：

- 最早的 **Microsoft.Data.SqlClient** 版本支援適用於 .NET Framework、.NET Core 與 .NET Standard 的 `Active Directory Password`。 該版本也支援適用於 .NET Framework 的 `Active Directory Integrated` 驗證與 `Active Directory Interactive` 驗證。 

- 從 **Microsoft.Data.SqlClient** 2.0.0 開始，已將對 `Active Directory Integrated` 驗證與 `Active Directory Interactive` 驗證的支援延伸到 .NET Framework、.NET Core 與 .NET Standard。 

  同時也在 SqlClient 2.0.0 中新增了新的 `Active Directory Service Principal` 驗證模式。 此模式會使用服務主體身分識別的用戶端識別碼與祕密來完成驗證。 

- **Microsoft.Data.SqlClient** 2.1.0 中新增了更多驗證模式，包括 `Active Directory Device Code Flow` 與 `Active Directory Managed Identity` (也稱為 `Active Directory MSI`)。 這些新模式可讓應用程式取得存取權杖以連線到伺服器。 

如果所需的 Azure AD 驗證相關資訊不在下列各節所述的範圍內，請參閱[使用 Azure Active Directory 驗證連線到 SQL Database](/azure/azure-sql/database/authentication-aad-overview)。


## <a name="setting-azure-active-directory-authentication"></a>設定 Azure Active Directory 驗證

使用 Azure AD 驗證來將應用程式連線到 Azure SQL 資料來源時，其必須提供有效的驗證模式。 下表列出支援的驗證模式。 應用程式會使用連接字串中的 `Authentication` 連線屬性來指定模式。

| 值 | 描述  | 架構    | Microsoft.Data.SqlClient 版本 |
|:--|:--|:--|:--:|
| Active Directory 密碼 | 利用使用者名稱與密碼，以 Azure AD 身分識別進行驗證 | .NET Framework 4.6+、.NET Core 2.1+、.NET Standard 2.0+  | 1.0+|
| Active Directory 整合式 |使用整合式驗證，以 Azure AD 身分識別進行驗證 | .NET Framework 4.6+、.NET Core 2.1+、.NET Standard 2.0+ | 2.0.0+<sup>1</sup> |
| Active Directory 互動式 | 使用互動式驗證，以 Azure AD 身分識別進行驗證 | .NET Framework 4.6+、.NET Core 2.1+、.NET Standard 2.0+ | 2.0.0+<sup>1</sup> |
| Active Directory 服務主體 | 使用服務主體身分識別的用戶端識別碼與祕密，以 Azure AD 身分識別進行驗證 | .NET Framework 4.6+、.NET Core 2.1+、.NET Standard 2.0+ | 2.0.0+ |
| Active Directory 裝置程式碼流程 | 使用裝置程式碼流程模式，以 Azure AD 身分識別進行驗證 | .NET Framework 4.6+、.NET Core 2.1+、.NET Standard 2.0+ | 2.1.0+ |
| Active Directory 受控識別、 <br>Active Directory MSI | 使用系統指派或使用者指派的受控識別，以 Azure AD 身分識別進行驗證 | .NET Framework 4.6+、.NET Core 2.1+、.NET Standard 2.0+ | 2.1.0+ |

<sup>1</sup> 在 **Microsoft.Data.SqlClient** 2.0.0 之前，`Active Directory Integrated` 與 `Active Directory Interactive` 驗證僅在 .NET Framework 4.6+ 上受到支援。 


## <a name="using-active-directory-password-authentication"></a>使用 Azure Active Directory 密碼驗證

`Active Directory Password` 驗證模式支援使用適用於原生或同盟 Azure AD 使用者的 Azure AD，來向 Azure 資料來源進行驗證。 當您使用此模式時，必須在連接字串中提供使用者認證。 下列範例示範如何使用 `Active Directory Password` 驗證。

```c#
// Use your own server, database, user ID, and password.
string ConnectionString = @"Server=demo.database.windows.net; Authentication=Active Directory Password; Database=testdb; User Id=user@domain.com; Password=**_";

using (SqlConnection conn = new SqlConnection(ConnectionString)) {
    conn.Open();
}
```


## <a name="using-active-directory-integrated-authentication"></a>使用 Active Directory 整合式驗證

若要使用 `Active Directory Integrated` 驗證模式，您必須為內部部署 Active Directory 執行個體與雲端中的 Azure AD 建立同盟。 例如，您可以使用 Active Directory 同盟服務 (AD FS) 建立同盟。

當您登入到已加入網域的機器時，便能存取 Azure SQL 資料來源，而不會使用此模式提示您提供認證。 您無法針對 .NET Framework 應用程式，在連接字串中指定使用者名稱與密碼。 使用者名稱在 .NET Core 與 .NET Standard 應用程式的連接字串中是選擇性的。 您無法在此模式中設定 SqlConnection 的 `Credential` 屬性。 

下列程式碼片段是使用 `Active Directory Integrated` 驗證時的範例。

```c#
// Use your own server and database.
string ConnectionString1 = @"Server=demo.database.windows.net; Authentication=Active Directory Integrated; Database=testdb";

using (SqlConnection conn = new SqlConnection(ConnectionString1)) {
    conn.Open();
}

// User ID is optional for .NET Core and .NET Standard.
string ConnectionString2 = @"Server=demo.database.windows.net; Authentication=Active Directory Integrated; Database=testdb; User Id=user@domain.com";

using (SqlConnection conn = new SqlConnection(ConnectionString2)) {
    conn.Open();
}
```


## <a name="using-active-directory-interactive-authentication"></a>使用 Active Directory 互動式驗證

`Active Directory Interactive` 驗證支援多重要素驗證技術，以連線到 Azure SQL 資料來源。 如果您在連接字串中提供此驗證模式，將會出現 Azure 驗證畫面，並要求使用者輸入有效的認證。 您無法在連接字串中指定密碼。 

您無法在此模式中設定 SqlConnection 的 `Credential` 屬性。 使用 _ *Microsoft.Data.SqlClient** 2.0.0 與更新版本，當您處於互動模式時，連接字串中允許使用者名稱。 

下列範例示範如何使用 `Active Directory Interactive` 驗證。

```c#
// Use your own server, database, and user ID.
// User ID is optional.
string ConnectionString1 = @"Server=demo.database.windows.net; Authentication=Active Directory Interactive; Database=testdb; User Id=user@domain.com";

using (SqlConnection conn = new SqlConnection(ConnectionString1)) {
    conn.Open();
}

// User ID is not provided.
string ConnectionString2 = @"Server=demo.database.windows.net; Authentication=Active Directory Interactive; Database=testdb";

using (SqlConnection conn = new SqlConnection(ConnectionString2)) {
    conn.Open();
}
```


## <a name="using-active-directory-service-principal-authentication"></a>使用 Azure Active Directory 服務主體驗證

在 `Active Directory Service Principal` 驗證模式中，用戶端應用程式可透過提供服務主體身分識別的用戶端識別碼與祕密來連線到 Azure SQL 資料來源。 服務主體驗證包括：
1. 使用祕密設定應用程式註冊。
1. 將權限授與 Azure SQL Database 執行個體中的應用程式。
1. 使用正確的認證進行連線。 

下列範例示範如何使用 `Active Directory Service Principal` 驗證。

```c#
// Use your own server, database, app ID, and secret.
string ConnectionString = @"Server=demo.database.windows.net; Authentication=Active Directory Service Principal; Database=testdb; User Id=AppId; Password=secret";

using (SqlConnection conn = new SqlConnection(ConnectionString)) {
    conn.Open();
}
```


## <a name="using-active-directory-device-code-flow-authentication"></a>使用 Active Directory 裝置程式碼流程驗證

使用適用於 .NET (MSAL.NET) 的 [Microsoft 驗證程式庫](/azure/active-directory/develop/msal-overview)時，`Active Directory Device Code Flow` 驗證可讓用戶端應用程式從不具互動式網頁瀏覽器的裝置與作業系統連線到 Azure SQL 資料來源。 互動式驗證將會在另一部裝置上執行。 如需裝置程式碼流程驗證的詳細資訊，請參閱 [OAuth 2.0 裝置程式碼流程](/azure/active-directory/develop/v2-oauth2-device-code)。 

使用此模式時，您無法設定 `SqlConnection` 的 `Credential` 屬性。 此外，也不能在連接字串中指定使用者名稱與密碼。 

下列程式碼片段是使用 `Active Directory Device Code Flow` 驗證的範例。

```c#
// Use your own server and database.
string ConnectionString = @"Server=demo.database.windows.net; Authentication=Active Directory Device Code Flow; Database=testdb";

using (SqlConnection conn = new SqlConnection(ConnectionString)) {
    conn.Open();
}
```


## <a name="using-active-directory-managed-identity-authentication"></a>使用 Azure Active Directory 受控識別驗證

先前稱為受控服務識別 (MSI) 的服務，其新名稱為「Azure 資源受控識別」。 當用戶端應用程式使用 Azure 資源來存取支援 Azure AD 驗證的 Azure 服務時，您可以在 Azure AD 中提供適用於 Azure 資源的身分識別，以使用受控識別進行驗證。 接著，您可以使用該身分識別來取得存取權杖。 這可降低管理認證與祕密的需求。 

受控身分識別有兩種： 

- 「系統指派的受控識別」可直接建立於 Azure AD 中的服務執行個體上。 其繫結至該服務執行個體的生命週期。 
- 「使用者指派的受控識別」會以獨立 Azure 資源的形式來建立。 其可指派給 Azure 服務的一或多個執行個體。 

如需受控識別的詳細資訊，請參閱[關於 Azure 資源受控識別](/azure/active-directory/managed-identities-azure-resources/overview)。

從 **Microsoft.Data.SqlClient** 2.1.0 開始，驅動程式可透過受控識別取得存取權杖，以支援向 Azure SQL Database、Azure Synapse Analytics 與 Azure SQL 受控執行個體進行驗證。 若要使用此驗證，請在連接字串中指定 `Active Directory Managed Identity` 或 `Active Directory MSI`，而且不需任何密碼。 

您也無法在此模式中設定 `SqlConnection` 的 `Credential` 屬性。 針對使用者指派的受控識別，則必須提供使用者名稱。 

下列範例示範如何搭配系統指派的受控識別使用 `Active Directory Managed Identity` 驗證。

```c#
// For system-assigned managed identity
// Use your own server and database.
string ConnectionString1 = @"Server=demo.database.windows.net; Authentication=Active Directory Managed Identity; Database=testdb";

using (SqlConnection conn = new SqlConnection(ConnectionString1)) {
    conn.Open();
}

string ConnectionString2 = @"Server=demo.database.windows.net; Authentication=Active Directory MSI; Database=testdb";

using (SqlConnection conn = new SqlConnection(ConnectionString2)) {
    conn.Open();
}
```

下列範例示範如何搭配使用者指派的受控識別使用 `Active Directory Managed Identity` 驗證。

```c#
// For user-assigned managed identity
// Use your own server, database, and user ID.
string ConnectionString1 = @"Server=demo.database.windows.net; Authentication=Active Directory Managed Identity; User Id=ObjectIdOfManagedIdentity; Database=testdb";

using (SqlConnection conn = new SqlConnection(ConnectionString1)) {
    conn.Open();
}

string ConnectionString2 = @"Server=demo.database.windows.net; Authentication=Active Directory MSI; User Id=ObjectIdOfManagedIdentity; Database=testdb";

using (SqlConnection conn = new SqlConnection(ConnectionString2)) {
    conn.Open();
}
```


## <a name="customizing-active-directory-authentication"></a>自訂 Active Directory 驗證

除了使用內建於驅動程式的 Active Directory 驗證之外，**Microsoft.Data.SqlClient** 2.1.0 與更新版本會為應用程式提供自訂 Active Directory 驗證的選項。 自訂會以 `ActiveDirectoryAuthenticationProvider` 類別為基礎，此類別衍生自 [`SqlAuthenticationProvider`](/dotnet/api/system.data.sqlclient.sqlauthenticationprovider) 抽象類別。 

在 Active Directory 驗證期間，用戶端應用程式可以透過下列方式定義自己的 `ActiveDirectoryAuthencationProvider` 類別：

- 使用自訂的回呼方法。
- 透過 SqlClient 驅動程式來將應用程式用戶端識別碼傳遞至 MSAL 程式庫，以擷取存取權杖。

下列範例示範如何在使用 `Active Directory Device Code Flow` 驗證時使用自訂回呼。 

[!code-csharp [AADAuthenticationCustomDeviceFlowCallback#1](~/../sqlclient/doc/samples/AADAuthenticationCustomDeviceFlowCallback.cs#1)]

使用自訂的 `ActiveDirectoryAuthenticationProvider` 類別，在使用支援的 Active Directory 驗證模式時，可將使用者定義的應用程式用戶端識別碼傳遞至 SqlClient。 支援的 Active Directory 驗證模式包括 `Active Directory Password`、`Active Directory Integrated`、`Active Directory Interactive`、`Active Directory Service Principal` 與 `Active Directory Device Code Flow`。

應用程式用戶端識別碼也可以透過 `SqlAuthenticationProviderConfigurationSection` 或 `SqlClientAuthenticationProviderConfigurationSection` 來設定。 設定屬性 `applicationClientId` 適用於 .NET Framework 4.6+ 與 .NET Core 2.1+。

下列程式碼片段是在使用 `Active Directory Interactive` 驗證時，搭配使用者定義的應用程式用戶端識別碼使用自訂 `ActiveDirectoryAuthenticationProvider` 類別的範例。

[!code-csharp [ApplicationClientIdAzureAuthenticationProvider#1](~/../sqlclient/doc/samples/ApplicationClientIdAzureAuthenticationProvider.cs#1)]

下列範例示範如何透過設定區段來設定應用程式用戶端識別碼。

```xml
<configuration>
  <configSections>
    <section name="SqlClientAuthenticationProviders"
             type="Microsoft.Data.SqlClient.SqlClientAuthenticationProviderConfigurationSection, Microsoft.Data.SqlClient" />
  </configSections>
  <SqlClientAuthenticationProviders applicationClientId ="<GUID>" />
</configuration>

<!--or-->

<configuration>
  <configSections>
    <section name="SqlAuthenticationProviders"
             type="Microsoft.Data.SqlClient.SqlAuthenticationProviderConfigurationSection, Microsoft.Data.SqlClient" />
  </configSections>
  <SqlAuthenticationProviders applicationClientId ="<GUID>" />
</configuration>
```

## <a name="support-for-a-custom-sql-authentication-provider"></a>支援自訂的 SQL 驗證提供者

透過更大的彈性，用戶端應用程式也可以使用自己的提供者來進行 Active Directory 驗證，而不需使用 `ActiveDirectoryAuthenticationProvider` 類別。 自訂驗證提供者必須是具有覆寫方法之 `SqlAuthenticationProvider` 的子類別。 

下列範例示範如何使用新的驗證提供者來進行 `Active Directory Device Code Flow` 驗證。

[!code-csharp [CustomDeviceCodeFlowAzureAuthenticationProvider#1](~/../sqlclient/doc/samples/CustomDeviceCodeFlowAzureAuthenticationProvider.cs#1)]

除了改進 `Active Directory Interactive` 驗證體驗之外，**Microsoft.Data.SqlClient** 2.1.0 與更新版本提供下列 API，讓用戶端應用程式自訂互動式驗證與裝置程式碼流程驗證。

```c#
public class ActiveDirectoryAuthenticationProvider
{
    // For .NET Framework targeted applications only
    // Sets a reference to the current System.Windows.Forms.IWin32Window that triggers the browser to be shown. 
    // Used to center the browser pop-up onto this window.
    public void SetIWin32WindowFunc(Func<IWin32Window> iWin32WindowFunc);

    // For .NET Standard targeted applications only
    // Sets a reference to the ViewController (if using Xamarin.iOS), Activity (if using Xamarin.Android) IWin32Window, or IntPtr (if using .NET Framework). 
    // Used for invoking the browser for Active Directory Interactive authentication.
    public void SetParentActivityOrWindowFunc(Func<object> parentActivityOrWindowFunc);

    // For .NET Framework, .NET Core, and .NET Standard targeted applications
    // Sets a callback method that's invoked with a custom web UI instance that will let the user sign in with Azure AD, present consent if needed, and get back the authorization code. 
    // Applicable when working with Active Directory Interactive authentication.
    public void SetAcquireAuthorizationCodeAsyncCallback(Func<Uri, Uri, CancellationToken, Task<Uri>> acquireAuthorizationCodeAsyncCallback);

    // For .NET Framework, .NET Core, and .NET Standard targeted applications
    // Clears cached user tokens from the token provider.
    public static void ClearUserTokenCache();
}
```


## <a name="see-also"></a>另請參閱
- [Azure Active Directory 中的應用程式和服務主體物件](/azure/active-directory/develop/app-objects-and-service-principals)
- [驗證流程](/azure/active-directory/develop/msal-authentication-flows)
