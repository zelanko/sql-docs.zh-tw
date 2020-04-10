---
title: Microsoft Drivers for PHP for SQL Server 的系統需求 | Microsoft Docs
ms.custom: ''
ms.date: 01/31/2020
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- requirements
ms.assetid: 5db4b75f-c605-4785-9560-399a533c0fc9
author: David-Engel
ms.reviewer: carlrab
ms.author: v-daenge
ms.openlocfilehash: 2e48fcb222575095fab4c313102de8abc4e3efa0
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80926862"
---
# <a name="system-requirements-for-the-microsoft-drivers-for-php-for-sql-server"></a>Microsoft Drivers for PHP for SQL Server 的系統需求

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

此文章列出要使用 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 來存取 SQL Server 或 Azure SQL Database 中的資料時，系統上必須安裝的元件。

Microsoft PHP Drivers for SQL Server 3.2 版和更新版本已正式支援。 如需有關支援生命週期和 PHP 驅動程式需求的完整詳細資訊，請參閱[支援矩陣](../../connect/php/microsoft-php-drivers-for-sql-server-support-matrix.md)。

## <a name="php"></a>PHP

如需如何下載及安裝最新的穩定 PHP 二進位檔的資訊，請參閱 [PHP 網站](https://php.net)。  Microsoft Drivers for PHP for SQL Server 需要正確版本的 PHP，如 [PHP 版本支援](../../connect/php/microsoft-php-drivers-for-sql-server-support-matrix.md#php-version-support)中所述。

-   必須使用對應的 PHP 版本來啟用驅動程式檔案的正確版本。 如需不同驅動程式檔案的相關資訊，請參閱[驅動程式版本](#driver-versions)。  若要載入驅動程式，請參閱[下載 Microsoft Drivers for PHP for SQL Server](../../connect/php/download-drivers-php-sql-server.md)。 如需為 PHP 設定驅動程式的資訊，請參閱[載入 Microsoft Drivers for PHP for SQL Server](../../connect/php/loading-the-php-sql-driver.md)。

-   需要 Web 伺服器。 您的 Web 伺服器必須設定為執行 PHP。 如需使用 IIS 裝載 PHP 應用程式的相關資訊，請參閱 [PHP 網站上的教學課程](http://docs.php.net/manual/da/install.windows.iis7.php) \(英文\)。

    [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 已使用 IIS 10 和 FastCGI 測試。

    > [!NOTE]
    > Microsoft 僅提供 IIS 的支援。

## <a name="odbc-driver"></a>ODBC 驅動程式

PHP 執行所在的電腦上需要正確版本的 Microsoft ODBC Driver for SQL Server。 您可以在[此頁面](https://docs.microsoft.com/sql/connect/odbc/download-odbc-driver-for-sql-server?view=sql-server-2017)上下載支援的平台之驅動程式的所有支援版本。

如果您要在 64 位元版本的 Windows 上下載 Windows 版本的驅動程式，ODBC 64 位元安裝程式會同時安裝 32 位元和 64 位元的 ODBC 驅動程式。 如果您使用 32 位元版本的 Windows，請使用 ODBC x86 安裝程式。 在非 Windows 平台上，只有 64 位元版本的驅動程式可供使用。

|適用於 SQL Server 的 PHP 驅動程式版本 &#8594;<br />&#8595; ODBC 驅動程式版本|5.8|5.6|5.3|5.2|4.3|4.0|3.2|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|ODBC 驅動程式 17+ |Y|Y|Y|Y| | | |
|ODBC 驅動程式 13.1|Y|Y|Y|Y|Y|Y| |
|ODBC Driver 13  | | | | | |Y| |
|ODBC Driver 11  |Y|Y|Y|Y|Y|Y|Y|

如果您使用 SQLSRV 驅動程式，[sqlsrv_client_info](../../connect/php/sqlsrv-client-info.md) 會傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正在使用哪個 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] Microsoft ODBC Driver for SQL Server 版本的相關資訊。 如果您使用 PDO_SQLSRV 驅動程式，您可以使用 [PDO::getAttribute](../../connect/php/pdo-getattribute.md) 來探索版本。

## <a name="sql-server"></a>SQL Server

如需搭配 Azure SQL Database 使用 PHP 的詳細資訊，請參閱[連接到 Microsoft Azure SQL Database](../../connect/php/connecting-to-microsoft-azure-sql-database.md)。

|適用於 SQL Server 的 PHP 驅動程式版本 &#8594;<br />&#8595; SQL Server 版本|5.8|5.6|5.3|5.2|4.3|4.0|3.2|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Azure SQL Database (所有部署選項)        |Y|Y|Y|Y| | | |
|Azure SQL Synapse  |Y|Y|Y|Y| | | |
|SQL Server 2019           |Y|Y|Y|Y| | | |
|SQL Server 2017           |Y|Y|Y|Y| | | |
|SQL Server 2016           |Y|Y|Y|Y|Y| | |
|SQL Server 2014           |Y|Y|Y|Y|Y|Y|Y|
|SQL Server 2012           |Y|Y|Y|Y|Y|Y|Y|
|SQL Server 2008 R2        | |Y|Y|Y|Y|Y|Y|
|SQL Server 2008           | | | | |Y|Y|Y|

## <a name="operating-systems"></a>作業系統

如需支援哪些作業系統的詳細資訊，請參閱[支援的作業系統](../../connect/php/microsoft-php-drivers-for-sql-server-support-matrix.md#supported-operating-systems)。

## <a name="driver-versions"></a>驅動程式版本

此節列出每個 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 版本中所包含的驅動程式檔案。 每個安裝套件都包含執行緒和非執行緒形式變體的 SQLSRV 和 PDO_SQLSRV 驅動程式檔案。 在 Windows 上，其也以 32 位元與 64 位元變體提供。 若要設定用於 PHP 執行階段的驅動程式，請遵循[載入 Microsoft Drivers for PHP for SQL Server](../../connect/php/loading-the-php-sql-driver.md) 中的安裝指示。

在支援的 Linux 和 macOS 版本上，可以使用 PHP 的 PECL 套件系統來安裝適當的驅動程式，請遵循 [Linux 和 macOS 安裝指示](../../connect/php/installation-tutorial-linux-mac.md)。 或者，您可以從 [Microsoft Drivers for PHP for SQL Server](https://github.com/Microsoft/msphpsql/releases) GitHub 專案頁面下載適用於您平台的預先建立的二進位套件 -- 下表列出在預先建立的二進位套件中找到的檔案。

**Microsoft Drivers 5.8 for PHP for SQL Server：**

在 Windows 上，會包含下列版本的驅動程式：

|驅動程式檔案|PHP 版本|具備執行緒安全性？|與 PHP .dll 搭配使用|
|---------------|:---------------:|:----------------:|---------------------|
|32-bit php_sqlsrv_72_nts.dll<br />32-bit php_pdo_sqlsrv_72_nts.dll|7.2|否 |32 位元 php7.dll|
|32-bit php_sqlsrv_72_ts.dll <br />32-bit php_pdo_sqlsrv_72_ts.dll |7.2|是|32 位元 php7ts.dll|
|64-bit php_sqlsrv_72_nts.dll<br />64-bit php_pdo_sqlsrv_72_nts.dll|7.2|否 |64 位元 php7.dll|
|64-bit php_sqlsrv_72_ts.dll <br />64-bit php_pdo_sqlsrv_72_ts.dll |7.2|是|64 位元 php7ts.dll|
|32-bit php_sqlsrv_73_nts.dll<br />32-bit php_pdo_sqlsrv_73_nts.dll|7.3|否 |32 位元 php7.dll|
|32-bit php_sqlsrv_73_ts.dll <br />32-bit php_pdo_sqlsrv_73_ts.dll |7.3|是|32 位元 php7ts.dll|
|64-bit php_sqlsrv_73_nts.dll<br />64-bit php_pdo_sqlsrv_73_nts.dll|7.3|否 |64 位元 php7.dll|
|64-bit php_sqlsrv_73_ts.dll <br />64-bit php_pdo_sqlsrv_73_ts.dll |7.3|是|64 位元 php7ts.dll|
|32 位元 php_sqlsrv_74_nts.dll<br />32 位元 php_pdo_sqlsrv_74_nts.dll|7.4|否 |32 位元 php7.dll|
|32 位元 php_sqlsrv_74_ts.dll <br />32 位元 php_pdo_sqlsrv_74_ts.dll |7.4|是|32 位元 php7ts.dll|
|64 位元 php_sqlsrv_74_nts.dll<br />64 位元 php_pdo_sqlsrv_74_nts.dll|7.4|否 |64 位元 php7.dll|
|64 位元 php_sqlsrv_74_ts.dll <br />64 位元 php_pdo_sqlsrv_74_ts.dll |7.4|是|64 位元 php7ts.dll|

在 Linux 上，會包含下列版本的驅動程式：

|驅動程式檔案|PHP 版本|具備執行緒安全性？|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_72_nts.so<br />php_pdo_sqlsrv_72_nts.so|7.2|否 |
|php_sqlsrv_72_ts.so <br />php_pdo_sqlsrv_72_ts.so |7.2|是|
|php_sqlsrv_73_nts.so<br />php_pdo_sqlsrv_73_nts.so|7.3|否 |
|php_sqlsrv_73_ts.so <br />php_pdo_sqlsrv_73_ts.so |7.3|是|
|php_sqlsrv_74_nts.so<br />php_pdo_sqlsrv_74_nts.so|7.4|否 |
|php_sqlsrv_74_ts.so <br />php_pdo_sqlsrv_74_ts.so |7.4|是|

**Microsoft Drivers 5.6 for PHP for SQL Server：**

在 Windows 上，會包含下列版本的驅動程式：

|驅動程式檔案|PHP 版本|具備執行緒安全性？|與 PHP .dll 搭配使用|
|---------------|:---------------:|:----------------:|---------------------|
|32-bit php_sqlsrv_71_nts.dll<br />32-bit php_pdo_sqlsrv_71_nts.dll|7.1|否 |32 位元 php7.dll|
|32-bit php_sqlsrv_71_ts.dll <br />32-bit php_pdo_sqlsrv_71_ts.dll |7.1|是|32 位元 php7ts.dll|
|64-bit php_sqlsrv_71_nts.dll<br />64-bit php_pdo_sqlsrv_71_nts.dll|7.1|否 |64 位元 php7.dll|
|64-bit php_sqlsrv_71_ts.dll <br />64-bit php_pdo_sqlsrv_71_ts.dll |7.1|是|64 位元 php7ts.dll|
|32-bit php_sqlsrv_72_nts.dll<br />32-bit php_pdo_sqlsrv_72_nts.dll|7.2|否 |32 位元 php7.dll|
|32-bit php_sqlsrv_72_ts.dll <br />32-bit php_pdo_sqlsrv_72_ts.dll |7.2|是|32 位元 php7ts.dll|
|64-bit php_sqlsrv_72_nts.dll<br />64-bit php_pdo_sqlsrv_72_nts.dll|7.2|否 |64 位元 php7.dll|
|64-bit php_sqlsrv_72_ts.dll <br />64-bit php_pdo_sqlsrv_72_ts.dll |7.2|是|64 位元 php7ts.dll|
|32-bit php_sqlsrv_73_nts.dll<br />32-bit php_pdo_sqlsrv_73_nts.dll|7.3|否 |32 位元 php7.dll|
|32-bit php_sqlsrv_73_ts.dll <br />32-bit php_pdo_sqlsrv_73_ts.dll |7.3|是|32 位元 php7ts.dll|
|64-bit php_sqlsrv_73_nts.dll<br />64-bit php_pdo_sqlsrv_73_nts.dll|7.3|否 |64 位元 php7.dll|
|64-bit php_sqlsrv_73_ts.dll <br />64-bit php_pdo_sqlsrv_73_ts.dll |7.3|是|64 位元 php7ts.dll|

在 Linux 上，會包含下列版本的驅動程式：

|驅動程式檔案|PHP 版本|具備執行緒安全性？|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|否 |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|是|
|php_sqlsrv_72_nts.so<br />php_pdo_sqlsrv_72_nts.so|7.2|否 |
|php_sqlsrv_72_ts.so <br />php_pdo_sqlsrv_72_ts.so |7.2|是|
|php_sqlsrv_73_nts.so<br />php_pdo_sqlsrv_73_nts.so|7.3|否 |
|php_sqlsrv_73_ts.so <br />php_pdo_sqlsrv_73_ts.so |7.3|是|

**Microsoft Drivers 5.3 for PHP for SQL Server：**

在 Windows 上，會包含下列版本的驅動程式：

|驅動程式檔案|PHP 版本|具備執行緒安全性？|與 PHP .dll 搭配使用|
|---------------|:---------------:|:----------------:|---------------------|
|32-bit php_sqlsrv_7_nts.dll <br />32-bit php_pdo_sqlsrv_7_nts.dll |7.0|否 |32 位元 php7.dll|
|32-bit php_sqlsrv_7_ts.dll  <br />32-bit php_pdo_sqlsrv_7_ts.dll  |7.0|是|32 位元 php7ts.dll|
|64-bit php_sqlsrv_7_nts.dll <br />64-bit php_pdo_sqlsrv_7_nts.dll |7.0|否 |64 位元 php7.dll|
|64-bit php_sqlsrv_7_ts.dll  <br />64-bit php_pdo_sqlsrv_7_ts.dll  |7.0|是|64 位元 php7ts.dll|
|32-bit php_sqlsrv_71_nts.dll<br />32-bit php_pdo_sqlsrv_71_nts.dll|7.1|否 |32 位元 php7.dll|
|32-bit php_sqlsrv_71_ts.dll <br />32-bit php_pdo_sqlsrv_71_ts.dll |7.1|是|32 位元 php7ts.dll|
|64-bit php_sqlsrv_71_nts.dll<br />64-bit php_pdo_sqlsrv_71_nts.dll|7.1|否 |64 位元 php7.dll|
|64-bit php_sqlsrv_71_ts.dll <br />64-bit php_pdo_sqlsrv_71_ts.dll |7.1|是|64 位元 php7ts.dll|
|32-bit php_sqlsrv_72_nts.dll<br />32-bit php_pdo_sqlsrv_72_nts.dll|7.2|否 |32 位元 php7.dll|
|32-bit php_sqlsrv_72_ts.dll <br />32-bit php_pdo_sqlsrv_72_ts.dll |7.2|是|32 位元 php7ts.dll|
|64-bit php_sqlsrv_72_nts.dll<br />64-bit php_pdo_sqlsrv_72_nts.dll|7.2|否 |64 位元 php7.dll|
|64-bit php_sqlsrv_72_ts.dll <br />64-bit php_pdo_sqlsrv_72_ts.dll |7.2|是|64 位元 php7ts.dll|

在 Linux 上，會包含下列版本的驅動程式：

|驅動程式檔案|PHP 版本|具備執行緒安全性？|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|否 |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|是|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|否 |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|是|
|php_sqlsrv_72_nts.so<br />php_pdo_sqlsrv_72_nts.so|7.2|否 |
|php_sqlsrv_72_ts.so <br />php_pdo_sqlsrv_72_ts.so |7.2|是|

**Microsoft Drivers 5.2 for PHP for SQL Server：**

在 Windows 上，會包含下列版本的驅動程式：

|驅動程式檔案|PHP 版本|具備執行緒安全性？|與 PHP .dll 搭配使用|
|---------------|:---------------:|:----------------:|---------------------|
|32-bit php_sqlsrv_7_nts.dll <br />32-bit php_pdo_sqlsrv_7_nts.dll |7.0|否 |32 位元 php7.dll|
|32-bit php_sqlsrv_7_ts.dll  <br />32-bit php_pdo_sqlsrv_7_ts.dll  |7.0|是|32 位元 php7ts.dll|
|64-bit php_sqlsrv_7_nts.dll <br />64-bit php_pdo_sqlsrv_7_nts.dll |7.0|否 |64 位元 php7.dll|
|64-bit php_sqlsrv_7_ts.dll  <br />64-bit php_pdo_sqlsrv_7_ts.dll  |7.0|是|64 位元 php7ts.dll|
|32-bit php_sqlsrv_71_nts.dll<br />32-bit php_pdo_sqlsrv_71_nts.dll|7.1|否 |32 位元 php7.dll|
|32-bit php_sqlsrv_71_ts.dll <br />32-bit php_pdo_sqlsrv_71_ts.dll |7.1|是|32 位元 php7ts.dll|
|64-bit php_sqlsrv_71_nts.dll<br />64-bit php_pdo_sqlsrv_71_nts.dll|7.1|否 |64 位元 php7.dll|
|64-bit php_sqlsrv_71_ts.dll <br />64-bit php_pdo_sqlsrv_71_ts.dll |7.1|是|64 位元 php7ts.dll|
|32-bit php_sqlsrv_72_nts.dll<br />32-bit php_pdo_sqlsrv_72_nts.dll|7.2|否 |32 位元 php7.dll|
|32-bit php_sqlsrv_72_ts.dll <br />32-bit php_pdo_sqlsrv_72_ts.dll |7.2|是|32 位元 php7ts.dll|
|64-bit php_sqlsrv_72_nts.dll<br />64-bit php_pdo_sqlsrv_72_nts.dll|7.2|否 |64 位元 php7.dll|
|64-bit php_sqlsrv_72_ts.dll <br />64-bit php_pdo_sqlsrv_72_ts.dll |7.2|是|64 位元 php7ts.dll|

在 Linux 上，會包含下列版本的驅動程式：

|驅動程式檔案|PHP 版本|具備執行緒安全性？|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|否 |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|是|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|否 |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|是|
|php_sqlsrv_72_nts.so<br />php_pdo_sqlsrv_72_nts.so|7.2|否 |
|php_sqlsrv_72_ts.so <br />php_pdo_sqlsrv_72_ts.so |7.2|是|

**Microsoft Drivers 4.3 for PHP for SQL Server：**

在 Windows 上，會包含下列版本的驅動程式：

|驅動程式檔案|PHP 版本|具備執行緒安全性？|與 PHP .dll 搭配使用|
|---------------|:---------------:|:----------------:|---------------------|
|32-bit php_sqlsrv_7_nts.dll <br />32-bit php_pdo_sqlsrv_7_nts.dll |7.0|否 |32 位元 php7.dll|
|32-bit php_sqlsrv_7_ts.dll  <br />32-bit php_pdo_sqlsrv_7_ts.dll  |7.0|是|32 位元 php7ts.dll|
|64-bit php_sqlsrv_7_nts.dll <br />64-bit php_pdo_sqlsrv_7_nts.dll |7.0|否 |64 位元 php7.dll|
|64-bit php_sqlsrv_7_ts.dll  <br />64-bit php_pdo_sqlsrv_7_ts.dll  |7.0|是|64 位元 php7ts.dll|
|32-bit php_sqlsrv_71_nts.dll<br />32-bit php_pdo_sqlsrv_71_nts.dll|7.1|否 |32 位元 php7.dll|
|32-bit php_sqlsrv_71_ts.dll <br />32-bit php_pdo_sqlsrv_71_ts.dll |7.1|是|32 位元 php7ts.dll|
|64-bit php_sqlsrv_71_nts.dll<br />64-bit php_pdo_sqlsrv_71_nts.dll|7.1|否 |64 位元 php7.dll|
|64-bit php_sqlsrv_71_ts.dll <br />64-bit php_pdo_sqlsrv_71_ts.dll |7.1|是|64 位元 php7ts.dll|

在 Linux 上，會包含下列版本的驅動程式：

|驅動程式檔案|PHP 版本|具備執行緒安全性？|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|否 |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|是|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|否 |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|是|

**Microsoft Drivers 4.0 for PHP for SQL Server：**

在 Windows 上，會包含下列版本的驅動程式：

|驅動程式檔案|PHP 版本|具備執行緒安全性？|與 PHP .dll 搭配使用|
|---------------|:---------------:|:----------------:|---------------------|
|php_sqlsrv_7_nts_x86.dll<br />php_pdo_sqlsrv_7_nts_x86.dll|7.0|否|32 位元 php7.dll|
|php_sqlsrv_7_ts_x86.dll<br />php_pdo_sqlsrv_7_ts_x86.dll|7.0|是|32 位元 php7ts.dll|
|php_sqlsrv_7_nts_x64.dll<br />php_pdo_sqlsrv_7_nts_x64.dll|7.0|否|64 位元 php7.dll|
|php_sqlsrv_7_ts_x64.dll<br />php_pdo_sqlsrv_7_ts_x64.dll|7.0|是|64 位元 php7ts.dll|

在 Linux 上，會包含下列版本的驅動程式：

|驅動程式檔案|PHP 版本|具備執行緒安全性？|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|否 |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|是|

**Microsoft Drivers 3.2 for PHP for SQL Server：**

在 Windows 上，會包含下列版本的驅動程式：

|驅動程式檔案|PHP 版本|具備執行緒安全性？|與 PHP .dll 搭配使用|
|---------------|:---------------:|:----------------:|---------------------|
|php_sqlsrv_54_nts.dll<br />php_pdo_sqlsrv_54_nts.dll|5.4|否|php5.dll|
|php_sqlsrv_54_ts.dll<br />php_pdo_sqlsrv_54_ts.dll|5.4|是|php5ts.dll|
|php_sqlsrv_55_nts.dll<br />php_pdo_sqlsrv_55_nts.dll|5.5|否|php5.dll|
|php_sqlsrv_55_ts.dll<br />php_pdo_sqlsrv_55_ts.dll|5.5|是|php5ts.dll|
|php_sqlsrv_56_nts.dll<br />php_pdo_sqlsrv_56_nts.dll|5.6|否|php5.dll|
|php_sqlsrv_56_ts.dll<br />php_pdo_sqlsrv_56_ts.dll|5.6|是|php5ts.dll|

## <a name="see-also"></a>另請參閱

- [開始使用 Microsoft Drivers for PHP for SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)
- [Microsoft Drivers for PHP for SQL Server 的程式設計指南](../../connect/php/programming-guide-for-php-sql-driver.md)
- [SQLSRV 驅動程式 API 參考](../../connect/php/sqlsrv-driver-api-reference.md)
- [PDO_SQLSRV 驅動程式 API 參考](../../connect/php/pdo-sqlsrv-driver-reference.md)
