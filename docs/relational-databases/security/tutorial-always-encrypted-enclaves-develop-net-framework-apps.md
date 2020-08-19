---
description: 教學課程：使用具有安全記憶體保護區的 Always Encrypted 開發 .NET Framework 應用程式
title: 教學課程：使用具有安全記憶體保護區的 Always Encrypted 開發 .NET Framework 應用程式 | Microsoft Docs
ms.custom: ''
ms.date: 10/15/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: cd75e0a63ebbfbf6a5749939442b8b8a2e964d92
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88403794"
---
# <a name="tutorial-develop-a-net-framework-application-using-always-encrypted-with-secure-enclaves"></a>教學課程：使用具有安全記憶體保護區的 Always Encrypted 開發 .NET Framework 應用程式
[!INCLUDE [sqlserver2019-windows-only](../../includes/applies-to-version/sqlserver2019-windows-only.md)]

本教學課程會教您如何開發簡單的應用程式來發出資料庫查詢，其使用[具有安全記憶體保護區 Always Encrypted](encryption/always-encrypted-enclaves.md) 的伺服器端安全記憶體保護區。 

## <a name="prerequisites"></a>必要條件
本教學課程是[教學課程：使用 SSMS，開始使用具有安全記憶體保護區的 Always Encrypted](./tutorial-getting-started-with-always-encrypted-enclaves.md)。 請確定您已完成它，再繼續進行下列步驟。

此外，您還需要 Visual Studio (建議使用版本 2019)；您可以從 [https://visualstudio.microsoft.com/](https://visualstudio.microsoft.com) 進行下載。 您的應用程式開發電腦必須執行 .NET Framework 4.7.2 或更新版本。

## <a name="step-1-set-up-your-visual-studio-project"></a>步驟 1:設定 Visual Studio 專案

若要在 .NET Framework 應用程式中使用具有安全記憶體保護區的 Always Encrypted，您需要確定應用程式是針對 .NET Framework 4.7.2 所建置，並已與 [Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders NuGet](https://www.nuget.org/packages/Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders) 相整合。 此外，如果您將資料行主要金鑰儲存至 Azure Key Vault，則也需要整合應用程式與 [Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider NuGet](https://www.nuget.org/packages/Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider)、版本 2.2.0 或更新版本。 

1. 開啟 Visual Studio。

2. 建立新的 C\# 主控台應用程式 (.NET Framework) 專案。

3. 請確定您專案的目標至少為 .NET Framework 4.7.2。 以滑鼠右鍵按一下 [方案總管] 中的專案，並選取 [屬性]，然後將 [目標架構] 設定為 .NET Framework 4.7.2。

4. 移至 [工具]\(主功能表) > [NuGet 套件管理員] > [套件管理員主控台]，以安裝下列 NuGet 套件。 在 [套件管理員主控台] 中，執行下列程式碼。

   ```powershell
   Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders -IncludePrerelease
   ```

5. 如果您使用 Azure Key Vault 來儲存資料行主要金鑰，請移至 [工具]\(主功能表) > [NuGet 套件管理員] > [套件管理員主控台]，以安裝下列 NuGet 套件。 在 [套件管理員主控台] 中，執行下列程式碼。

   ```powershell
   Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider -IncludePrerelease -Version 2.2.0
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   ```

7. 開啟您專案的 App.config 檔。

8. 找到 \<configuration\> 區段，然後新增或更新這些 \<configSections\> 區段。

   a. 若 \<configuration\> 區段**不**包含 \<configSections\> 區段，請緊接在 \<configuration\> 的下方新增下列內容。
   
      ```xml
      <configSections>
         <section name="SqlColumnEncryptionEnclaveProviders" type="System.Data.SqlClient.SqlColumnEncryptionEnclaveProviderConfigurationSection, System.Data, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />
      </configSections>
      ```
   b. 如果 \<configruation\> 區段已包含 \<configSections\> 區段，請在 \<configSections\> 內新增下行程式碼：

   ```xml
   <section name="SqlColumnEncryptionEnclaveProviders"  type="System.Data.SqlClient.SqlColumnEncryptionEnclaveProviderConfigurationSection, System.Data,  Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" /\>
   ```

9. 在組態區段的 \<configSections\> 下方，新增下列區段，以指定要用來證明以及與 VBS 記憶體保護區互動的記憶體保護區提供者：

   ```xml
   <SqlColumnEncryptionEnclaveProviders>
       <providers>
           <add name="VBS"  type="Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders.HostGuardianServiceEnclaveProvider,  Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders,    Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91"/>
       </providers>
   </SqlColumnEncryptionEnclaveProviders>
   ```

以下是簡易主控台應用程式之 app.config 檔案的完整範例。
```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <configSections>
    <section name="SqlColumnEncryptionEnclaveProviders" type="System.Data.SqlClient.SqlColumnEncryptionEnclaveProviderConfigurationSection, System.Data, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />
  </configSections>
  <SqlColumnEncryptionEnclaveProviders>
    <providers>
      <add name="VBS"  type="Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders.HostGuardianServiceEnclaveProvider,  Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders,    Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91"/>
    </providers>
  </SqlColumnEncryptionEnclaveProviders>
  <startup> 
    <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.7.2" />
  </startup>
</configuration>
```
## <a name="step-2-implement-your-application-logic"></a>步驟 2:實作您的應用程式邏輯
您的應用程式將會連線到 **ContosoHR** 資料庫 (來自[教學課程：使用 SSMS 開始使用具有安全記憶體保護區的 Always Encrypted](tutorial-getting-started-with-always-encrypted-enclaves.md))，並會執行查詢，其中包含在 **SSN** 資料行上的 `LIKE` 述詞和 **Salary** 資料行上的範圍比較。

1. 將 Program.cs 檔案 (由 Visual Studio 產生) 的內容替換成以下程式碼。 使用您伺服器名稱和環境的記憶體保護區證明 URL 來更新資料庫連接字串。 您也可以更新資料庫驗證設定。

    ```cs
    using System;
    using System.Data.SqlClient;
    using System.Data;

    namespace ConsoleApp1
    {
        class Program
        {
            static void Main(string[] args)
            {
    
                string connectionString = "Data Source = myserver; Initial Catalog = ContosoHR; Column Encryption Setting = Enabled;Enclave Attestation Url = http://hgs.bastion.local/Attestation; Integrated Security = true";

                using (SqlConnection connection = new SqlConnection(connectionString))
                {
                    connection.Open();

                    SqlCommand cmd = connection.CreateCommand();
                    cmd.CommandText = @"SELECT [SSN], [FirstName], [LastName], [Salary] FROM [dbo].[Employees] WHERE [SSN] LIKE @SSNPattern AND [Salary] > @MinSalary;";

                    SqlParameter paramSSNPattern = cmd.CreateParameter();

                    paramSSNPattern.ParameterName = @"@SSNPattern";
                    paramSSNPattern.DbType = DbType.AnsiStringFixedLength;
                    paramSSNPattern.Direction = ParameterDirection.Input;
                    paramSSNPattern.Value = "%1111";
                    paramSSNPattern.Size = 11;

                    cmd.Parameters.Add(paramSSNPattern);

                    SqlParameter MinSalary = cmd.CreateParameter();

                    MinSalary.ParameterName = @"@MinSalary";
                    MinSalary.DbType = DbType.Currency;
                    MinSalary.Direction = ParameterDirection.Input;
                    MinSalary.Value = 900;

                    cmd.Parameters.Add(MinSalary);
                    cmd.ExecuteNonQuery();
    
                    SqlDataReader reader = cmd.ExecuteReader();
                    while (reader.Read())

                    {
                        Console.WriteLine(reader);
                        Console.WriteLine(reader[0] + ", " + reader[1] + ", " + reader[2] + ", " + reader[3]);
                    }   
                    Console.ReadKey();
                }
            }
        }
    }
    ```
2. 建置並執行應用程式。  

## <a name="see-also"></a>另請參閱
- [搭配 .NET Framework Data Provider for SQL Server 使用 [永遠加密]](encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)
