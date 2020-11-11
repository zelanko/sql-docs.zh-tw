---
title: Oracle 連線類型 (SSRS 和 Power BI 報表伺服器)
description: 請運用本文中有關 Oracle 連線類型的資訊，以了解如何建立資料來源。
ms.date: 11/03/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: 9db86dd2-beda-42d8-8af7-2629d58a8e3d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: f92b7e0a414cbe6b9cbdb9dcc04cc8779ff4cff6
ms.sourcegitcommit: 985e2e8e494badeac6d6b652cd35765fd9c12d80
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/04/2020
ms.locfileid: "93328470"
---
# <a name="oracle-connection-type-ssrs--power-bi-report-server"></a>Oracle 連線類型 (SSRS 和 Power BI 報表伺服器)

若要在報表中使用來自 Oracle 資料庫的資料，您必須具有以 Oracle 類型的報表資料來源為基礎的資料集。 此內建資料來源類型會直接使用 Oracle 資料提供者，並且需要 Oracle 用戶端軟體元件。 本文說明如何下載及安裝 Reporting Services、Power BI 報表伺服器、報表產生器和 Power BI Desktop 的驅動程式。


您可使用本文中的資訊來建置資料來源。 如需逐步指示，請參閱 [加入及驗證資料連接 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)。 

> [!IMPORTANT]
> 下列提供的命令使用 Oracle 的 OraProvCfg.exe 工具來註冊 Oracle 受控和非受控 ODP.NET 驅動程式，可作為搭配上述 Microsoft 產品使用的範例。 若要設定環境特定的 ODP.NET 驅動程式，您可能需要連絡 Oracle 支援人員，或參考 Oracle 的文件：[Configuring Oracle Data Provider for .NET](https://docs.oracle.com/en/database/oracle/oracle-database/19/odpnt/InstallConfig.html#GUID-1F689B90-2CC4-4907-B8FE-A5F4EE36F673) (設定 Oracle Data Provider for .NET)。

## <a name="64-bit-drivers-for-the-report-servers"></a>適用於報表伺服器的 64 位元驅動程式

在 Oracle 下載網站上，安裝 [Oracle 64-bit ODAC Oracle Universal Installer (OUI)](https://www.oracle.com/technetwork/topics/dotnet/downloads/odacdeploy-4242173.html)。 只有在使用 Oracle ODAC 驅動程式 12.2 和更新版本時，才需要執行下列步驟。 否則，預設會對新 Oracle 主目錄的非電腦全域組態安裝這些驅動程式。 這些步驟假設您已將 ODAC 18.x 檔案安裝至 c:\oracle64 資料夾。


### <a name="paginated-rdl-reports-use-managed-odpnet"></a>編頁 (RDL) 報表使用受控 ODP.NET

Power BI 報表伺服器以及 SQL Server Reporting Services 2016 和更新版本都使用 **受控 ODP.NET** 來撰寫編頁 (RDL) 報表。 請遵循這些步驟來註冊受控 ODP.NET：

1. 向 GAC 註冊 ODP.NET 受控用戶端：

   ```
   C:\oracle64\product\18.0.0\client_1\odp.net\bin\4\OraProvCfg.exe /action:gac /providerpath:C:\oracle64\product\18.0.0\client_1\odp.net\managed\common\Oracle.ManagedDataAccess.dll
   ```

2. 將 ODP.NET 受控用戶端項目新增至 machine.config：

   ```
   C:\oracle64\product\18.0.0\client_1\odp.net\bin\4\OraProvCfg.exe /action:config /force /product:odpm /frameworkversion:v4.0.30319 /providerpath:C:\oracle64\product\18.0.0\client_1\odp.net\managed\common\Oracle.ManagedDataAccess.dll
   ```

### <a name="power-bi-reports-use-unmanaged-odpnet"></a>Power BI 報表使用非受控 ODP.NET

Power BI 報表伺服器使用 **非受控 ODP.NET** 來撰寫 Power BI 報表。 遵循這些步驟來註冊非受控 ODP.NET：

1. 向 GAC 註冊 ODP.NET 受控用戶端：

   ```
   C:\oracle64\product\18.0.0\client_1\odp.net\bin\4\OraProvCfg.exe /action:gac /providerpath:C:\oracle64\product\18.0.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll
   ```
2. 將 ODP.NET 非受控用戶端項目新增至 machine.config：

   ```
   C:\oracle64\product\18.0.0\client_1\odp.net\bin\4\OraProvCfg.exe /action:config /force /product:odp /frameworkversion:v4.0.30319 /providerpath:C:\oracle64\product\18.0.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll
   ```

## <a name="32-bit-drivers-for-report-builder"></a>適用於報表產生器的 32 位元驅動程式

報表產生器使用 **受控 ODP.NET** 來撰寫編頁 (RDL) 報表。 只有在使用 Oracle ODAC 驅動程式 12.2 和更新版本時，才需要執行下列步驟。 否則，預設會對新 Oracle 主目錄的非電腦全域組態安裝這些驅動程式。 這些步驟假設您已將 ODAC 18.x 檔案安裝至報表產生器安裝所在的 c:\oracle32 資料夾。 請遵循這些步驟來註冊受控 ODP.NET：

1. 在 Oracle 下載網站上，安裝 [Oracle 32-bit ODAC Oracle Universal Installer (OUI)](https://www.oracle.com/technetwork/topics/dotnet/downloads/odacdev-4242174.html)。

2. 向 GAC 註冊 ODP.NET 受控用戶端：

   ```
   C:\oracle32\product\18.0.0\client_1\odp.net\bin\4\OraProvCfg.exe /action:gac /providerpath:C:\oracle32\product\18.0.0\client_1\odp.net\managed\common\Oracle.ManagedDataAccess.dll
   ```

3. 將 ODP.NET 受控用戶端項目新增至 machine.config：

   ```
   C:\oracle32\product\18.0.0\client_1\odp.net\bin\4\OraProvCfg.exe /action:config /force /product:odpm /frameworkversion:v4.0.30319 /providerpath:C:\oracle32\product\18.0.0\client_1\odp.net\managed\common\Oracle.ManagedDataAccess.dll
   ```

## <a name="64-bit-and-32-bit-drivers-for-power-bi-desktop"></a>Power BI Desktop 的 64 位元和 32 位元驅動程式

Power BI Desktop 使用 **非受控 ODP.NET** 來撰寫 Power BI 報表。 只有在使用 Oracle ODAC 驅動程式 12.2 和更新版本時，才需要執行下列步驟。 否則，預設會對新 Oracle 主目錄的非電腦全域組態安裝這些驅動程式。 這些步驟假設您已將 ODAC 18.x 檔案安裝至 c:\oracle64 資料夾 (適用於 64 位元 Power BI Desktop) 或 c:\oracle32 資料夾 (適用於 32 位元 Power BI Desktop)。 遵循這些步驟來註冊非受控 ODP.NET：

### <a name="64-bit-power-bi-desktop"></a>64 位元 Power BI Desktop

1. 在 Oracle 下載網站上，安裝 [Oracle 64-bit ODAC Oracle Universal Installer (OUI)](https://www.oracle.com/technetwork/topics/dotnet/downloads/odacdeploy-4242173.html)。
2. 向 GAC 註冊 ODP.NET 受控用戶端：

   ```
   C:\oracle64\product\18.0.0\client_1\odp.net\bin\4\OraProvCfg.exe /action:gac /providerpath:C:\oracle64\product\18.0.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll
   ```

3. 將 ODP.NET 非受控用戶端項目新增至 machine.config：

   ```
   C:\oracle64\product\18.0.0\client_1\odp.net\bin\4\OraProvCfg.exe /action:config /force /product:odp /frameworkversion:v4.0.30319 /providerpath:C:\oracle64\product\18.0.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll
   ```

### <a name="32-bit-power-bi-desktop"></a>32 位元 Power BI Desktop

1. 在 Oracle 下載網站上，安裝 [Oracle 32-bit ODAC Oracle Universal Installer (OUI)](https://www.oracle.com/technetwork/topics/dotnet/downloads/odacdev-4242174.html)。

2. 向 GAC 註冊 ODP.NET 受控用戶端：

   ```
   C:\oracle32\product\18.0.0\client_1\odp.net\bin\4\OraProvCfg.exe /action:gac /providerpath:C:\oracle32\product\18.0.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll
   ```

3. 將 ODP.NET 非受控用戶端項目新增至 machine.config：

   ```
   C:\oracle32\product\18.0.0\client_1\odp.net\bin\4\OraProvCfg.exe /action:config /force /product:odp /frameworkversion:v4.0.30319 /providerpath:C:\oracle32\product\18.0.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll
   ```

##  <a name="connection-string"></a><a name="Connection"></a> 連接字串  

請洽詢資料庫管理員，以取得用來連接資料來源的連接資訊和認證。 下列連接字串範例會使用 Unicode 來指定名為 "Oracle18" 之伺服器上的 Oracle 資料庫。 伺服器名稱必須符合 Tnsnames.ora 組態檔中定義為 Oracle 伺服器執行個體名稱的內容。  
  
```  
Data Source="Oracle"; Unicode="True"  
```  
  
如需詳細的連接字串範例，請參閱[建立資料連接字串 - 報表產生器 & SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)。  
  
##  <a name="credentials"></a><a name="Credentials"></a> 認證  
需要有認證才能夠執行報表、於本機預覽報表並且從報表伺服器預覽報表。  
  
發行報表之後，您可能需要變更資料來源的認證，如此當報表在報表伺服器上執行時，擷取資料的權限就會是有效的。  
  
如需詳細資訊，請參閱 [指定報表資料來源的認證及連接資訊](specify-credential-and-connection-information-for-report-data-sources.md)。  
  
##  <a name="queries"></a><a name="Query"></a> 查詢  
若要建立資料集，您可以從下拉式清單中選取預存程序，或是建立 SQL 查詢。 若要建立查詢，您必須使用以文字為基礎的查詢設計工具。 如需詳細資訊，請參閱[以文字為基礎的查詢設計工具使用者介面 &#40;報表產生器&#41;](../../reporting-services/report-data/text-based-query-designer-user-interface-report-builder.md)。  
  
您可以指定只傳回一個結果集的預存程序。 不支援使用以資料指標為基礎的查詢。  
  
##  <a name="parameters"></a><a name="Parameters"></a> 參數  

如果查詢包含查詢變數，就會自動產生對應的報表參數。 此延伸模組支援具名參數。 若使用 Oracle 9 或更新版本，則支援多重值的參數。  
  
 報表參數是透過預設屬性值建立，您可能會需要修改這些值。 例如，每一個報表參數的資料類型都是 **[文字]** 。 建立報表參數後，您可能必須變更預設值。 如需詳細資訊，請參閱 MSDN 上的 [報表參數 &#40;報表產生器和報表設計師&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)類型之報表資料來源為基礎的資料集。  
  
##  <a name="remarks"></a><a name="Remarks"></a> 備註  

系統管理員必須先安裝支援從 Oracle 資料庫擷取資料的 .NET Data Provider for Oracle 版本，您才能夠連接 Oracle 資料來源。 此資料提供者必須與報表產生器安裝在同一部電腦上，並且同樣位於報表伺服器上。  
  
如需詳細資訊，請參閱下列文章：  
  
- [如何使用 Reporting Services 設定及存取 Oracle 資料來源 (機器翻譯)](/archive/blogs/dataaccesstechnologies/configure-oracle-data-source-for-sql-server-reporting-services-ssdt-and-report-server)  
- [如何新增 NETWORK SERVICE 安全性主體的權限 (機器翻譯)](https://support.microsoft.com/kb/870668)  
  
### <a name="alternate-data-extensions"></a>替代資料延伸模組 

您也可以使用 OLE DB 資料來源類型，從 Oracle 資料庫擷取資料。 如需詳細資訊，請參閱 [OLE DB 連接類型 &#40;SSRS&#41;](../../reporting-services/report-data/ole-db-connection-type-ssrs.md)。  

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions" 

### <a name="report-models"></a>報表模型

 您也可以根據 Oracle 資料庫建立模型。  
::: moniker-end

### <a name="platform-and-version-information"></a>平台和版本資訊  

如需平台與版本支援的詳細資訊，請參閱 [Reporting Services &#40;SSRS&#41; 支援的資料來源](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)。  

## <a name="see-also"></a>另請參閱

[報表參數 &#40;報表產生器和報表設計師&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   

[篩選、分組和排序資料 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   

[運算式 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)
