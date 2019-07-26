---
title: Microsoft Drivers for PHP for SQL Server 的系統需求 | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- requirements
ms.assetid: 5db4b75f-c605-4785-9560-399a533c0fc9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b601d4fbb02b489aca228acb719cfe8bad834dc0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992575"
---
# <a name="system-requirements-for-the-microsoft-drivers-for-php-for-sql-server"></a>Microsoft Drivers for PHP for SQL Server 的系統需求
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本檔列出必須安裝在您的系統上, 才能使用[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]SQL Server 或 Azure SQL Database 中的資料來存取的元件。

適用于 SQL Server 的 Microsoft PHP 驅動程式3.1 版和更新版本已正式支援。 如需有關支援生命週期和需求 (包括舊版 PHP 驅動程式) 的完整詳細資料, 請參閱[支援矩陣](../../connect/php/microsoft-php-drivers-for-sql-server-support-matrix.md)。

## <a name="php"></a>PHP

如需如何下載及安裝最新的穩定 PHP 二進位檔的資訊，請參閱 [PHP 網站](https://php.net)。  適用于 PHP for SQL Server 的 Microsoft 驅動程式需要下列版本的 PHP:

|適用于 SQL Server 驅動程式版本的 PHP&#8594;<br />&#8595; PHP 版本|5.6|5.3|5.2|4.3|4.0|3.2|3.1|
|:---:|---|---|---|---|---|---|---|
|7.3|7.3.0+ | | | | | | |
|7.2|7.2+<sup>1</sup>|7.2+<sup>1</sup>|7.2+<sup>1</sup>| | | | |
|7.1|7.1.0+ |7.1.0+ |7.1.0+ |7.1.0+ |       |        |        |
|7.0|       |7.0.0+ |7.0.0+ |7.0.0+ |7.0.0+ |        |        |
|5.6|       |       |       |       |       |5.6.4+  |        |
|5.5|       |       |       |       |       |5.5.16+ |5.5.16+ |
|5.4|       |       |       |       |       |5.4.32  |5.4.32  |

1. Windows 支援7.2.1 和更新版本, 而 Linux 和 macOS 的版本7.2.0 和更新版本則受到支援。

-   您的 PHP 延伸目錄中必須要有某個版本的驅動程式檔案。 如需不同驅動程式檔案的相關資訊, 請參閱[驅動程式版本](#driver-versions)。  若要載入驅動程式，請參閱[下載 Microsoft Drivers for PHP for SQL Server](../../connect/php/download-drivers-php-sql-server.md)。 如需為 PHP 設定驅動程式的資訊，請參閱[載入 Microsoft Drivers for PHP for SQL Server](../../connect/php/loading-the-php-sql-driver.md)。

-   需要 Web 伺服器。 您的 Web 伺服器必須設定為執行 PHP。 如需使用 IIS 裝載 PHP 應用程式的相關資訊, 請參閱[PHP 網站上的教學](http://docs.php.net/manual/da/install.windows.iis7.php)課程。

    [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 已使用 IIS 10 和 FastCGI 測試。  

    > [!NOTE]  
    > Microsoft 僅提供 IIS 的支援。  

## <a name="odbc-driver"></a>ODBC 驅動程式

PHP 執行所在的電腦上需要正確的 Microsoft ODBC Driver for SQL Server 版本。 您可以在[此頁面](https://docs.microsoft.com/sql/connect/odbc/download-odbc-driver-for-sql-server?view=sql-server-2017)下載支援的平臺之驅動程式的所有支援版本。

如果您要在64位版本的 Windows 上下載 Windows 版本的驅動程式, ODBC 64 位安裝程式會同時安裝32位和64位的 ODBC 驅動程式。 如果您使用32位版本的 Windows, 請使用 ODBC x86 安裝程式。 在非 Windows 平臺上, 只有64位版本的驅動程式可供使用。

|適用于 SQL Server 驅動程式版本的 PHP&#8594;<br />&#8595; ODBC 驅動程式版本|5.6|5.3|5.2|4.3|4.0|3.2|3.1|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|ODBC 驅動程式 17+ |Y|Y|Y| | | | |
|ODBC 驅動程式 13.1|Y|Y|Y|Y|Y| | |
|ODBC Driver 13  | | | | |Y| | |
|ODBC Driver 11  |Y|Y|Y|Y|Y|Y|Y|

如果您使用 SQLSRV 驅動程式, [sqlsrv_client_info](../../connect/php/sqlsrv-client-info.md)會傳回所使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]之 Microsoft ODBC Driver for SQL Server 版本的相關資訊。 如果您使用 PDO_SQLSRV 驅動程式，您可以使用 [PDO::getAttribute](../../connect/php/pdo-getattribute.md) 來探索版本。  

## <a name="sql-server"></a>SQL Server

支援 Azure SQL 資料庫。 如需詳細資訊，請參閱[連接到 Microsoft Azure SQL Database](../../connect/php/connecting-to-microsoft-azure-sql-database.md)。

|適用于 SQL Server 驅動程式版本的 PHP&#8594;<br />&#8595; SQL Server 版本|5.6|5.3|5.2|4.3|4.0|3.2|3.1|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Azure SQL Database        |Y|Y|Y|Y| | | |
|Azure SQL 受控執行個體|Y|Y|Y|Y| | | |
|Azure SQL 資料倉儲  |Y|Y|Y|Y| | | |
|SQL Server 2017           |Y|Y|Y|Y| | | |
|SQL Server 2016           |Y|Y|Y|Y|Y| | |
|SQL Server 2014           |Y|Y|Y|Y|Y|Y|Y|
|SQL Server 2012           |Y|Y|Y|Y|Y|Y|Y|
|SQL Server 2008 R2        |Y|Y|Y|Y|Y|Y|Y|
|SQL Server 2008           | | | | |Y|Y|Y|

## <a name="operating-systems"></a>作業系統
針對每個版本的驅動程式支援的作業系統如下所示:

|適用于 SQL Server 驅動程式版本的 PHP&#8594;<br />&#8595; 作業系統|5.6|5.3|5.2|4.3|4.0|3.2|3.1|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Windows Server 2016                 |Y  |Y  |Y  |Y  |   |   |   |
|Windows Server 2012 R2              |Y  |Y  |Y  |Y  |Y  |Y  |Y  |
|Windows Server 2012                 |Y  |Y  |Y  |Y  |Y  |Y  |Y  |
|Windows Server 2008 R2 SP1          |   |   |   |   |Y  |Y  |Y  |
|Windows Server 2008 SP2             |   |   |   |   |Y  |Y  |Y  |
|Windows 10                          |Y  |Y  |Y  |Y  |Y  |   |   |
|Windows 8.1                         |Y  |Y  |Y  |Y  |Y  |Y  |Y  |
|Windows 8                           |   |   |   |Y  |Y  |Y  |Y  |
|Windows 7 SP1                       |   |   |   |   |Y  |Y  |Y  |
|Windows Vista SP2                   |   |   |   |   |Y  |Y  |Y  |
|Ubuntu 18.10 (64 位)               |Y  |   |   |   |   |   |   |
|Ubuntu 18.04 (64 位)               |Y  |Y  |   |   |   |   |   |
|Ubuntu 17.10 (64 位)               |   |Y  |Y  |   |   |   |   |
|Ubuntu 16.04 (64 位)               |Y  |Y  |Y  |Y  |Y  |   |   |
|Ubuntu 15.10 (64 位)               |   |   |   |Y  |   |   |   |
|Ubuntu 15.04 (64 位)               |   |   |   |   |Y  |   |   |
|Debian 9 (64 位)                   |Y  |Y  |Y  |   |   |   |   |
|Debian 8 (64 位)                   |Y  |Y  |Y  |Y  |   |   |   |
|Red Hat Enterprise Linux 7 (64 位元) |Y  |Y  |Y  |Y  |Y  |   |   |
|Suse Enterprise Linux 15 (64 位)   |Y  |   |   |   |   |   |   |
|Suse Enterprise Linux 12 (64 位)   |Y  |Y  |Y  |   |   |   |   |
|macOS Mojave (64 位)               |Y  |   |   |   |   |   |   |
|macOS 高塞拉里昂 (64 位)          |Y  |Y  |   |   |   |   |   |
|macOS Sierra (64 位)               |Y  |Y  |Y  |Y  |   |   |   |
|macOS El Capitan (64 位)           |   |Y  |Y  |Y  |   |   |   |

## <a name="driver-versions"></a>驅動程式版本  
本節列出每個版本[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]隨附的驅動程式檔案。 每個安裝套件都包含以執行緒和非執行緒形式變體的 SQLSRV 和 PDO_SQLSRV 驅動程式檔案。 在 Windows 上, 它們也可以在32位和64位的變數中使用。 若要設定與 PHP 執行時間搭配使用的驅動程式, 請依照載入適用于[php 的 Microsoft 驅動程式](../../connect/php/loading-the-php-sql-driver.md)中的安裝指示進行 SQL Server。

在支援的 Linux 和 macOS 版本上, 可以使用 PHP 的 PECL 套件系統來安裝適當的驅動程式, 請遵循[Linux 和 macOS 安裝指示](../../connect/php/installation-tutorial-linux-mac.md)。 或者, 您也可以從適用于 PHP for SQL Server Github 專案頁面的[Microsoft 驅動程式](https://github.com/Microsoft/msphpsql/releases)下載適用于您平臺的預建二進位檔--下表列出在預先建立的二進位封裝中找到的檔案。

**Microsoft Drivers 5.6 for PHP for SQL Server：**  

在 Windows 上, 會包含下列驅動程式版本:

|驅動程式檔案|PHP 版本|具備執行緒安全性？|與 PHP .dll 搭配使用|  
|---------------|:---------------:|:----------------:|---------------------|  
|32-bit php_sqlsrv_71_nts.dll<br />32-bit php_pdo_sqlsrv_71_nts.dll|7.1|否 |32-bit php7 .dll|  
|32-bit php_sqlsrv_71_ts.dll <br />32-bit php_pdo_sqlsrv_71_ts.dll |7.1|是|32-bit php7ts .dll|  
|64-bit php_sqlsrv_71_nts.dll<br />64-bit php_pdo_sqlsrv_71_nts.dll|7.1|否 |64-bit php7 .dll|  
|64-bit php_sqlsrv_71_ts.dll <br />64-bit php_pdo_sqlsrv_71_ts.dll |7.1|是|64-bit php7ts .dll|   
|32-bit php_sqlsrv_72_nts.dll<br />32-bit php_pdo_sqlsrv_72_nts.dll|7.2|否 |32-bit php7 .dll|  
|32-bit php_sqlsrv_72_ts.dll <br />32-bit php_pdo_sqlsrv_72_ts.dll |7.2|是|32-bit php7ts .dll|  
|64-bit php_sqlsrv_72_nts.dll<br />64-bit php_pdo_sqlsrv_72_nts.dll|7.2|否 |64-bit php7 .dll|  
|64-bit php_sqlsrv_72_ts.dll <br />64-bit php_pdo_sqlsrv_72_ts.dll |7.2|是|64-bit php7ts .dll|  
|32-bit php_sqlsrv_73_nts.dll<br />32-bit php_pdo_sqlsrv_73_nts.dll|7.3|否 |32-bit php7 .dll|  
|32-bit php_sqlsrv_73_ts.dll <br />32-bit php_pdo_sqlsrv_73_ts.dll |7.3|是|32-bit php7ts .dll|  
|64-bit php_sqlsrv_73_nts.dll<br />64-bit php_pdo_sqlsrv_73_nts.dll|7.3|否 |64-bit php7 .dll|  
|64-bit php_sqlsrv_73_ts.dll <br />64-bit php_pdo_sqlsrv_73_ts.dll |7.3|是|64-bit php7ts .dll|  

在 Linux 上, 會包含下列驅動程式版本:

|驅動程式檔案|PHP 版本|具備執行緒安全性？|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|否 |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|是|  
|php_sqlsrv_72_nts.so<br />php_pdo_sqlsrv_72_nts.so|7.2|否 |
|php_sqlsrv_72_ts.so <br />php_pdo_sqlsrv_72_ts.so |7.2|是|
|php_sqlsrv_73_nts.so<br />php_pdo_sqlsrv_73_nts.so|7.3|否 |
|php_sqlsrv_73_ts.so <br />php_pdo_sqlsrv_73_ts.so |7.3|是|

**Microsoft Drivers 5.3 for PHP for SQL Server：**  

在 Windows 上, 會包含下列驅動程式版本:

|驅動程式檔案|PHP 版本|具備執行緒安全性？|與 PHP .dll 搭配使用|  
|---------------|:---------------:|:----------------:|---------------------|  
|32-bit php_sqlsrv_7_nts.dll <br />32-bit php_pdo_sqlsrv_7_nts.dll |7.0|否 |32-bit php7 .dll|
|32-bit php_sqlsrv_7_ts.dll  <br />32-bit php_pdo_sqlsrv_7_ts.dll  |7.0|是|32-bit php7ts .dll|
|64-bit php_sqlsrv_7_nts.dll <br />64-bit php_pdo_sqlsrv_7_nts.dll |7.0|否 |64-bit php7 .dll|  
|64-bit php_sqlsrv_7_ts.dll  <br />64-bit php_pdo_sqlsrv_7_ts.dll  |7.0|是|64-bit php7ts .dll|
|32-bit php_sqlsrv_71_nts.dll<br />32-bit php_pdo_sqlsrv_71_nts.dll|7.1|否 |32-bit php7 .dll|  
|32-bit php_sqlsrv_71_ts.dll <br />32-bit php_pdo_sqlsrv_71_ts.dll |7.1|是|32-bit php7ts .dll|  
|64-bit php_sqlsrv_71_nts.dll<br />64-bit php_pdo_sqlsrv_71_nts.dll|7.1|否 |64-bit php7 .dll|  
|64-bit php_sqlsrv_71_ts.dll <br />64-bit php_pdo_sqlsrv_71_ts.dll |7.1|是|64-bit php7ts .dll|   
|32-bit php_sqlsrv_72_nts.dll<br />32-bit php_pdo_sqlsrv_72_nts.dll|7.2|否 |32-bit php7 .dll|  
|32-bit php_sqlsrv_72_ts.dll <br />32-bit php_pdo_sqlsrv_72_ts.dll |7.2|是|32-bit php7ts .dll|  
|64-bit php_sqlsrv_72_nts.dll<br />64-bit php_pdo_sqlsrv_72_nts.dll|7.2|否 |64-bit php7 .dll|  
|64-bit php_sqlsrv_72_ts.dll <br />64-bit php_pdo_sqlsrv_72_ts.dll |7.2|是|64-bit php7ts .dll|  

在 Linux 上, 會包含下列驅動程式版本:

|驅動程式檔案|PHP 版本|具備執行緒安全性？|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|否 |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|是|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|否 |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|是|  
|php_sqlsrv_72_nts.so<br />php_pdo_sqlsrv_72_nts.so|7.2|否 |
|php_sqlsrv_72_ts.so <br />php_pdo_sqlsrv_72_ts.so |7.2|是|

**Microsoft Drivers 5.2 for PHP for SQL Server：**  

在 Windows 上, 會包含下列驅動程式版本:

|驅動程式檔案|PHP 版本|具備執行緒安全性？|與 PHP .dll 搭配使用|  
|---------------|:---------------:|:----------------:|---------------------|  
|32-bit php_sqlsrv_7_nts.dll <br />32-bit php_pdo_sqlsrv_7_nts.dll |7.0|否 |32-bit php7 .dll|
|32-bit php_sqlsrv_7_ts.dll  <br />32-bit php_pdo_sqlsrv_7_ts.dll  |7.0|是|32-bit php7ts .dll|
|64-bit php_sqlsrv_7_nts.dll <br />64-bit php_pdo_sqlsrv_7_nts.dll |7.0|否 |64-bit php7 .dll|  
|64-bit php_sqlsrv_7_ts.dll  <br />64-bit php_pdo_sqlsrv_7_ts.dll  |7.0|是|64-bit php7ts .dll|
|32-bit php_sqlsrv_71_nts.dll<br />32-bit php_pdo_sqlsrv_71_nts.dll|7.1|否 |32-bit php7 .dll|  
|32-bit php_sqlsrv_71_ts.dll <br />32-bit php_pdo_sqlsrv_71_ts.dll |7.1|是|32-bit php7ts .dll|  
|64-bit php_sqlsrv_71_nts.dll<br />64-bit php_pdo_sqlsrv_71_nts.dll|7.1|否 |64-bit php7 .dll|  
|64-bit php_sqlsrv_71_ts.dll <br />64-bit php_pdo_sqlsrv_71_ts.dll |7.1|是|64-bit php7ts .dll|   
|32-bit php_sqlsrv_72_nts.dll<br />32-bit php_pdo_sqlsrv_72_nts.dll|7.2|否 |32-bit php7 .dll|  
|32-bit php_sqlsrv_72_ts.dll <br />32-bit php_pdo_sqlsrv_72_ts.dll |7.2|是|32-bit php7ts .dll|  
|64-bit php_sqlsrv_72_nts.dll<br />64-bit php_pdo_sqlsrv_72_nts.dll|7.2|否 |64-bit php7 .dll|  
|64-bit php_sqlsrv_72_ts.dll <br />64-bit php_pdo_sqlsrv_72_ts.dll |7.2|是|64-bit php7ts .dll|  

在 Linux 上, 會包含下列驅動程式版本:

|驅動程式檔案|PHP 版本|具備執行緒安全性？|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|否 |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|是|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|否 |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|是|  
|php_sqlsrv_72_nts.so<br />php_pdo_sqlsrv_72_nts.so|7.2|否 |
|php_sqlsrv_72_ts.so <br />php_pdo_sqlsrv_72_ts.so |7.2|是|

**Microsoft Drivers 4.3 for PHP for SQL Server：**  

在 Windows 上, 會包含下列驅動程式版本:

|驅動程式檔案|PHP 版本|具備執行緒安全性？|與 PHP .dll 搭配使用|  
|---------------|:---------------:|:----------------:|---------------------|  
|32-bit php_sqlsrv_7_nts.dll <br />32-bit php_pdo_sqlsrv_7_nts.dll |7.0|否 |32-bit php7 .dll|
|32-bit php_sqlsrv_7_ts.dll  <br />32-bit php_pdo_sqlsrv_7_ts.dll  |7.0|是|32-bit php7ts .dll|
|64-bit php_sqlsrv_7_nts.dll <br />64-bit php_pdo_sqlsrv_7_nts.dll |7.0|否 |64-bit php7 .dll|  
|64-bit php_sqlsrv_7_ts.dll  <br />64-bit php_pdo_sqlsrv_7_ts.dll  |7.0|是|64-bit php7ts .dll|
|32-bit php_sqlsrv_71_nts.dll<br />32-bit php_pdo_sqlsrv_71_nts.dll|7.1|否 |32-bit php7 .dll|  
|32-bit php_sqlsrv_71_ts.dll <br />32-bit php_pdo_sqlsrv_71_ts.dll |7.1|是|32-bit php7ts .dll|  
|64-bit php_sqlsrv_71_nts.dll<br />64-bit php_pdo_sqlsrv_71_nts.dll|7.1|否 |64-bit php7 .dll|  
|64-bit php_sqlsrv_71_ts.dll <br />64-bit php_pdo_sqlsrv_71_ts.dll |7.1|是|64-bit php7ts .dll|   

在 Linux 上, 會包含下列驅動程式版本:

|驅動程式檔案|PHP 版本|具備執行緒安全性？|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|否 |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|是|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|否 |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|是|  

**Microsoft Drivers 4.0 for PHP for SQL Server：**  

在 Windows 上, 會包含下列驅動程式版本:

|驅動程式檔案|PHP 版本|具備執行緒安全性？|與 PHP .dll 搭配使用|  
|---------------|:---------------:|:----------------:|---------------------|  
|php_sqlsrv_7_nts_x86.dll<br />php_pdo_sqlsrv_7_nts_x86.dll|7.0|否|32-bit php7 .dll|  
|php_sqlsrv_7_ts_x86.dll<br />php_pdo_sqlsrv_7_ts_x86.dll|7.0|是|32-bit php7ts .dll|  
|php_sqlsrv_7_nts_x64.dll<br />php_pdo_sqlsrv_7_nts_x64.dll|7.0|否|64-bit php7 .dll|  
|php_sqlsrv_7_ts_x64.dll<br />php_pdo_sqlsrv_7_ts_x64.dll|7.0|是|64-bit php7ts .dll|   

在 Linux 上, 會包含下列驅動程式版本:

|驅動程式檔案|PHP 版本|具備執行緒安全性？|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|否 |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|是|

**Microsoft Drivers 3.2 for PHP for SQL Server：**  

在 Windows 上, 會包含下列驅動程式版本:

|驅動程式檔案|PHP 版本|具備執行緒安全性？|與 PHP .dll 搭配使用|  
|---------------|:---------------:|:----------------:|---------------------|  
|php_sqlsrv_54_nts.dll<br />php_pdo_sqlsrv_54_nts.dll|5.4|否|php5.dll|  
|php_sqlsrv_54_ts.dll<br />php_pdo_sqlsrv_54_ts.dll|5.4|是|php5ts.dll|  
|php_sqlsrv_55_nts.dll<br />php_pdo_sqlsrv_55_nts.dll|5.5|否|php5.dll|  
|php_sqlsrv_55_ts.dll<br />php_pdo_sqlsrv_55_ts.dll|5.5|是|php5ts.dll|  
|php_sqlsrv_56_nts.dll<br />php_pdo_sqlsrv_56_nts.dll|5.6|否|php5.dll|  
|php_sqlsrv_56_ts.dll<br />php_pdo_sqlsrv_56_ts.dll|5.6|是|php5ts.dll|  

**Microsoft Drivers 3.1 for PHP for SQL Server：**  

在 Windows 上, 會包含下列驅動程式版本:

|驅動程式檔案|PHP 版本|具備執行緒安全性？|與 PHP .dll 搭配使用|  
|---------------|:---------------:|:----------------:|---------------------|  
|php_sqlsrv_54_nts.dll<br />php_pdo_sqlsrv_54_nts.dll|5.4|否|php5.dll|  
|php_sqlsrv_54_ts.dll<br />php_pdo_sqlsrv_54_ts.dll|5.4|是|php5ts.dll|  
|php_sqlsrv_55_nts.dll<br />php_pdo_sqlsrv_55_nts.dll|5.5|否|php5.dll|  
|php_sqlsrv_55_ts.dll<br />php_pdo_sqlsrv_55_ts.dll|5.5|是|php5ts.dll|  

## <a name="see-also"></a>另請參閱  
[開始使用 Microsoft Drivers for PHP for SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Microsoft Drivers for PHP for SQL Server 的程式設計指南](../../connect/php/programming-guide-for-php-sql-driver.md)

[SQLSRV 驅動程式 API 參考](../../connect/php/sqlsrv-driver-api-reference.md)

[PDO_SQLSRV 驅動程式 API 參考](../../connect/php/pdo-sqlsrv-driver-reference.md)  
