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
manager: craigg
ms.openlocfilehash: d53a3233d2e2af6aa9806cdea06b2a203e31bf89
ms.sourcegitcommit: 706f3a89fdb98e84569973f35a3032f324a92771
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2019
ms.locfileid: "58658410"
---
# <a name="system-requirements-for-the-microsoft-drivers-for-php-for-sql-server"></a>Microsoft Drivers for PHP for SQL Server 的系統需求
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本文件列出必須在您將存取資料的 SQL Server 或 Azure SQL Database 使用的系統安裝的元件[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]。

3.1 和更新版本的 Microsoft PHP Driver for SQL Server 版本正式支援。 如需完整有關支援週期和需求包括較早版本的 PHP 驅動程式的詳細資訊，請參閱[支援矩陣](../../connect/php/microsoft-php-drivers-for-sql-server-support-matrix.md)。

## <a name="php"></a>PHP

如需如何下載及安裝最新的穩定 PHP 二進位檔的資訊，請參閱 [PHP 網站](https://php.net)。  Microsoft Drivers for PHP for SQL Server 需要下列的 PHP 版本：

|PHP for SQL Server 驅動程式版本&#8594;<br />&#8595; PHP 版本|5.6|5.3|5.2|4.3|4.0|3.2|3.1|
|:---:|---|---|---|---|---|---|---|
|7.3|7.3.0+ | | | | | | |
|7.2|7.2+<sup>1</sup>|7.2+<sup>1</sup>|7.2+<sup>1</sup>| | | | |
|7.1|7.1.0+ |7.1.0+ |7.1.0+ |7.1.0+ |       |        |        |
|7.0|       |7.0.0+ |7.0.0+ |7.0.0+ |7.0.0+ |        |        |
|5.6|       |       |       |       |       |5.6.4+  |        |
|5.5|       |       |       |       |       |5.5.16+ |5.5.16+ |
|5.4|       |       |       |       |       |5.4.32  |5.4.32  |

1. 7.2.1 版本和更新版本才支援在 Windows，而版本 7.2.0 和更新版本才支援在 Linux 和 macOS 上。

-   您的 PHP 延伸目錄中必須要有某個版本的驅動程式檔案。 請參閱[驅動程式版本](#driver-versions)針對不同的驅動程式檔案的相關資訊。  若要載入驅動程式，請參閱[下載 Microsoft Drivers for PHP for SQL Server](../../connect/php/download-drivers-php-sql-server.md)。 如需為 PHP 設定驅動程式的資訊，請參閱[載入 Microsoft Drivers for PHP for SQL Server](../../connect/php/loading-the-php-sql-driver.md)。

-   需要 Web 伺服器。 您的 Web 伺服器必須設定為執行 PHP。 如需裝載 IIS 與 PHP 應用程式的資訊，請參閱[PHP 的網站上的教學課程](http://docs.php.net/manual/da/install.windows.iis7.php)。

    [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 已使用 IIS 10 和 FastCGI 測試。  

    > [!NOTE]  
    > Microsoft 僅提供 IIS 的支援。  

## <a name="odbc-driver"></a>ODBC 驅動程式

PHP 執行所在電腦上需要 Microsoft ODBC Driver for SQL Server 的正確版本。 您可以下載所有支援的版本的驅動程式支援的平台上[本頁](https://docs.microsoft.com/sql/connect/odbc/download-odbc-driver-for-sql-server?view=sql-server-2017)。

如果您要下載此驅動程式在 64 位元版本的 Windows 上的 Windows 版本，則 ODBC 64 位元安裝程式會安裝 32 位元和 64 位元 ODBC 驅動程式。 如果您使用 32 位元版本的 Windows，使用 ODBC x86 安裝程式。 非 Windows 平台上，只有 64 位元版本的驅動程式可用。

|PHP for SQL Server 驅動程式版本&#8594;<br />&#8595;ODBC 驅動程式版本|5.6|5.3|5.2|4.3|4.0|3.2|3.1|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|ODBC 驅動程式 17+ |Y|Y|Y| | | | |
|ODBC 驅動程式 13.1|Y|Y|Y|Y|Y| | |
|ODBC Driver 13  | | | | |Y| | |
|ODBC Driver 11  |Y|Y|Y|Y|Y|Y|Y|

如果您使用 SQLSRV 驅動程式時， [sqlsrv_client_info](../../connect/php/sqlsrv-client-info.md)傳回的版本資訊[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]正在使用 Microsoft ODBC Driver for SQL Server [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]。 如果您使用 PDO_SQLSRV 驅動程式，您可以使用 [PDO::getAttribute](../../connect/php/pdo-getattribute.md) 來探索版本。  

## <a name="sql-server"></a>SQL Server

支援 azure SQL 資料庫。 如需詳細資訊，請參閱[連接到 Microsoft Azure SQL Database](../../connect/php/connecting-to-microsoft-azure-sql-database.md)。

|PHP for SQL Server 驅動程式版本&#8594;<br />&#8595; SQL Server 版本|5.6|5.3|5.2|4.3|4.0|3.2|3.1|
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
每個版本的驅動程式支援的作業系統如下所示：

|PHP for SQL Server 驅動程式版本&#8594;<br />&#8595; 作業系統|5.6|5.3|5.2|4.3|4.0|3.2|3.1|
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
|Ubuntu 18.10 （64 位元）               |Y  |   |   |   |   |   |   |
|Ubuntu 18.04 （64 位元）               |Y  |Y  |   |   |   |   |   |
|Ubuntu 17.10 （64 位元）               |   |Y  |Y  |   |   |   |   |
|Ubuntu 16.04 （64 位元）               |Y  |Y  |Y  |Y  |Y  |   |   |
|Ubuntu 15.10 （64 位元）               |   |   |   |Y  |   |   |   |
|Ubuntu 15.04 （64 位元）               |   |   |   |   |Y  |   |   |
|Debian 9 （64 位元）                   |Y  |Y  |Y  |   |   |   |   |
|Debian 8 （64 位元）                   |Y  |Y  |Y  |Y  |   |   |   |
|Red Hat Enterprise Linux 7 (64 位元) |Y  |Y  |Y  |Y  |Y  |   |   |
|Suse Enterprise Linux 15 （64 位元）   |Y  |   |   |   |   |   |   |
|Suse Enterprise Linux 12 （64 位元）   |Y  |Y  |Y  |   |   |   |   |
|macOS Mojave （64 位元）               |Y  |   |   |   |   |   |   |
|macOS High Sierra （64 位元）          |Y  |Y  |   |   |   |   |   |
|macOS Sierra （64 位元）               |Y  |Y  |Y  |Y  |   |   |   |
|macOS El Capitan （64 位元）           |   |Y  |Y  |Y  |   |   |   |

## <a name="driver-versions"></a>驅動程式版本  
此區段會列出隨附的每個版本的驅動程式檔案[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]。 每個安裝套件包含執行緒及非執行緒變體的 SQLSRV 和 PDO_SQLSRV 驅動程式檔案。 在 Windows 中，它們也會提供 32 位元和 64 位元的變體。 若要設定 PHP 執行階段使用的驅動程式，請依照下列中的安裝指示[Loading the Microsoft Drivers for PHP，適用於 SQL Server](../../connect/php/loading-the-php-sql-driver.md)。

在 Linux 和 macOS 的支援版本，適當的驅動程式可以安裝使用 PHP 的 PECL 封裝系統，下列[Linux 和 macOS 安裝指示](../../connect/php/installation-tutorial-linux-mac.md)。 或者，您可以在這裡下載預先建置的二進位檔從您的平台[Microsoft Drivers for PHP for SQL Server](https://github.com/Microsoft/msphpsql/releases) Github 專案頁面下方的表格列出預先建置的二進位封裝中的檔案。

**Microsoft Drivers 5.6 for PHP for SQL Server：**  

在 Windows 中，下列版本的驅動程式會包含：

|驅動程式檔案|PHP 版本|具備執行緒安全性？|與 PHP .dll 搭配使用|  
|---------------|:---------------:|:----------------:|---------------------|  
|32 位元 php_sqlsrv_71_nts.dll<br />32-bit php_pdo_sqlsrv_71_nts.dll|7.1|否 |32 位元 php7.dll|  
|32-bit php_sqlsrv_71_ts.dll <br />32-bit php_pdo_sqlsrv_71_ts.dll |7.1|是|32 位元 php7ts.dll|  
|64 位元 php_sqlsrv_71_nts.dll<br />64-bit php_pdo_sqlsrv_71_nts.dll|7.1|否 |64 位元 php7.dll|  
|64-bit php_sqlsrv_71_ts.dll <br />64-bit php_pdo_sqlsrv_71_ts.dll |7.1|是|64 位元 php7ts.dll|   
|32-bit php_sqlsrv_72_nts.dll<br />32-bit php_pdo_sqlsrv_72_nts.dll|7.2|否 |32 位元 php7.dll|  
|32-bit php_sqlsrv_72_ts.dll <br />32-bit php_pdo_sqlsrv_72_ts.dll |7.2|是|32 位元 php7ts.dll|  
|64-bit php_sqlsrv_72_nts.dll<br />64-bit php_pdo_sqlsrv_72_nts.dll|7.2|否 |64 位元 php7.dll|  
|64-bit php_sqlsrv_72_ts.dll <br />64-bit php_pdo_sqlsrv_72_ts.dll |7.2|是|64 位元 php7ts.dll|  
|32 位元 php_sqlsrv_73_nts.dll<br />32-bit php_pdo_sqlsrv_73_nts.dll|7.3|否 |32 位元 php7.dll|  
|32-bit php_sqlsrv_73_ts.dll <br />32-bit php_pdo_sqlsrv_73_ts.dll |7.3|是|32 位元 php7ts.dll|  
|64 位元 php_sqlsrv_73_nts.dll<br />64-bit php_pdo_sqlsrv_73_nts.dll|7.3|否 |64 位元 php7.dll|  
|64-bit php_sqlsrv_73_ts.dll <br />64-bit php_pdo_sqlsrv_73_ts.dll |7.3|是|64 位元 php7ts.dll|  

在 Linux 上，下列版本的驅動程式會包含：

|驅動程式檔案|PHP 版本|具備執行緒安全性？|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|否 |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|是|  
|php_sqlsrv_72_nts.so<br />php_pdo_sqlsrv_72_nts.so|7.2|否 |
|php_sqlsrv_72_ts.so <br />php_pdo_sqlsrv_72_ts.so |7.2|是|
|php_sqlsrv_73_nts.so<br />php_pdo_sqlsrv_73_nts.so|7.3|否 |
|php_sqlsrv_73_ts.so <br />php_pdo_sqlsrv_73_ts.so |7.3|是|

**Microsoft Drivers 5.3 for PHP for SQL Server：**  

在 Windows 中，下列版本的驅動程式會包含：

|驅動程式檔案|PHP 版本|具備執行緒安全性？|與 PHP .dll 搭配使用|  
|---------------|:---------------:|:----------------:|---------------------|  
|32 位元 php_sqlsrv_7_nts.dll <br />32-bit php_pdo_sqlsrv_7_nts.dll |7.0|否 |32 位元 php7.dll|
|32 位元 php_sqlsrv_7_ts.dll  <br />32-bit php_pdo_sqlsrv_7_ts.dll  |7.0|是|32 位元 php7ts.dll|
|64 位元 php_sqlsrv_7_nts.dll <br />64-bit php_pdo_sqlsrv_7_nts.dll |7.0|否 |64 位元 php7.dll|  
|64 位元 php_sqlsrv_7_ts.dll  <br />64-bit php_pdo_sqlsrv_7_ts.dll  |7.0|是|64 位元 php7ts.dll|
|32 位元 php_sqlsrv_71_nts.dll<br />32-bit php_pdo_sqlsrv_71_nts.dll|7.1|否 |32 位元 php7.dll|  
|32-bit php_sqlsrv_71_ts.dll <br />32-bit php_pdo_sqlsrv_71_ts.dll |7.1|是|32 位元 php7ts.dll|  
|64 位元 php_sqlsrv_71_nts.dll<br />64-bit php_pdo_sqlsrv_71_nts.dll|7.1|否 |64 位元 php7.dll|  
|64-bit php_sqlsrv_71_ts.dll <br />64-bit php_pdo_sqlsrv_71_ts.dll |7.1|是|64 位元 php7ts.dll|   
|32-bit php_sqlsrv_72_nts.dll<br />32-bit php_pdo_sqlsrv_72_nts.dll|7.2|否 |32 位元 php7.dll|  
|32-bit php_sqlsrv_72_ts.dll <br />32-bit php_pdo_sqlsrv_72_ts.dll |7.2|是|32 位元 php7ts.dll|  
|64-bit php_sqlsrv_72_nts.dll<br />64-bit php_pdo_sqlsrv_72_nts.dll|7.2|否 |64 位元 php7.dll|  
|64-bit php_sqlsrv_72_ts.dll <br />64-bit php_pdo_sqlsrv_72_ts.dll |7.2|是|64 位元 php7ts.dll|  

在 Linux 上，下列版本的驅動程式會包含：

|驅動程式檔案|PHP 版本|具備執行緒安全性？|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|否 |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|是|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|否 |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|是|  
|php_sqlsrv_72_nts.so<br />php_pdo_sqlsrv_72_nts.so|7.2|否 |
|php_sqlsrv_72_ts.so <br />php_pdo_sqlsrv_72_ts.so |7.2|是|

**Microsoft Drivers 5.2 for PHP for SQL Server：**  

在 Windows 中，下列版本的驅動程式會包含：

|驅動程式檔案|PHP 版本|具備執行緒安全性？|與 PHP .dll 搭配使用|  
|---------------|:---------------:|:----------------:|---------------------|  
|32 位元 php_sqlsrv_7_nts.dll <br />32-bit php_pdo_sqlsrv_7_nts.dll |7.0|否 |32 位元 php7.dll|
|32 位元 php_sqlsrv_7_ts.dll  <br />32-bit php_pdo_sqlsrv_7_ts.dll  |7.0|是|32 位元 php7ts.dll|
|64 位元 php_sqlsrv_7_nts.dll <br />64-bit php_pdo_sqlsrv_7_nts.dll |7.0|否 |64 位元 php7.dll|  
|64 位元 php_sqlsrv_7_ts.dll  <br />64-bit php_pdo_sqlsrv_7_ts.dll  |7.0|是|64 位元 php7ts.dll|
|32 位元 php_sqlsrv_71_nts.dll<br />32-bit php_pdo_sqlsrv_71_nts.dll|7.1|否 |32 位元 php7.dll|  
|32-bit php_sqlsrv_71_ts.dll <br />32-bit php_pdo_sqlsrv_71_ts.dll |7.1|是|32 位元 php7ts.dll|  
|64 位元 php_sqlsrv_71_nts.dll<br />64-bit php_pdo_sqlsrv_71_nts.dll|7.1|否 |64 位元 php7.dll|  
|64-bit php_sqlsrv_71_ts.dll <br />64-bit php_pdo_sqlsrv_71_ts.dll |7.1|是|64 位元 php7ts.dll|   
|32-bit php_sqlsrv_72_nts.dll<br />32-bit php_pdo_sqlsrv_72_nts.dll|7.2|否 |32 位元 php7.dll|  
|32-bit php_sqlsrv_72_ts.dll <br />32-bit php_pdo_sqlsrv_72_ts.dll |7.2|是|32 位元 php7ts.dll|  
|64-bit php_sqlsrv_72_nts.dll<br />64-bit php_pdo_sqlsrv_72_nts.dll|7.2|否 |64 位元 php7.dll|  
|64-bit php_sqlsrv_72_ts.dll <br />64-bit php_pdo_sqlsrv_72_ts.dll |7.2|是|64 位元 php7ts.dll|  

在 Linux 上，下列版本的驅動程式會包含：

|驅動程式檔案|PHP 版本|具備執行緒安全性？|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|否 |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|是|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|否 |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|是|  
|php_sqlsrv_72_nts.so<br />php_pdo_sqlsrv_72_nts.so|7.2|否 |
|php_sqlsrv_72_ts.so <br />php_pdo_sqlsrv_72_ts.so |7.2|是|

**Microsoft Drivers 4.3 for PHP for SQL Server：**  

在 Windows 中，下列版本的驅動程式會包含：

|驅動程式檔案|PHP 版本|具備執行緒安全性？|與 PHP .dll 搭配使用|  
|---------------|:---------------:|:----------------:|---------------------|  
|32 位元 php_sqlsrv_7_nts.dll <br />32-bit php_pdo_sqlsrv_7_nts.dll |7.0|否 |32 位元 php7.dll|
|32 位元 php_sqlsrv_7_ts.dll  <br />32-bit php_pdo_sqlsrv_7_ts.dll  |7.0|是|32 位元 php7ts.dll|
|64 位元 php_sqlsrv_7_nts.dll <br />64-bit php_pdo_sqlsrv_7_nts.dll |7.0|否 |64 位元 php7.dll|  
|64 位元 php_sqlsrv_7_ts.dll  <br />64-bit php_pdo_sqlsrv_7_ts.dll  |7.0|是|64 位元 php7ts.dll|
|32 位元 php_sqlsrv_71_nts.dll<br />32-bit php_pdo_sqlsrv_71_nts.dll|7.1|否 |32 位元 php7.dll|  
|32-bit php_sqlsrv_71_ts.dll <br />32-bit php_pdo_sqlsrv_71_ts.dll |7.1|是|32 位元 php7ts.dll|  
|64 位元 php_sqlsrv_71_nts.dll<br />64-bit php_pdo_sqlsrv_71_nts.dll|7.1|否 |64 位元 php7.dll|  
|64-bit php_sqlsrv_71_ts.dll <br />64-bit php_pdo_sqlsrv_71_ts.dll |7.1|是|64 位元 php7ts.dll|   

在 Linux 上，下列版本的驅動程式會包含：

|驅動程式檔案|PHP 版本|具備執行緒安全性？|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|否 |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|是|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|否 |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|是|  

**Microsoft Drivers 4.0 for PHP for SQL Server：**  

在 Windows 中，下列版本的驅動程式會包含：

|驅動程式檔案|PHP 版本|具備執行緒安全性？|與 PHP .dll 搭配使用|  
|---------------|:---------------:|:----------------:|---------------------|  
|php_sqlsrv_7_nts_x86.dll<br />php_pdo_sqlsrv_7_nts_x86.dll|7.0|否|32 位元 php7.dll|  
|php_sqlsrv_7_ts_x86.dll<br />php_pdo_sqlsrv_7_ts_x86.dll|7.0|是|32 位元 php7ts.dll|  
|php_sqlsrv_7_nts_x64.dll<br />php_pdo_sqlsrv_7_nts_x64.dll|7.0|否|64 位元 php7.dll|  
|php_sqlsrv_7_ts_x64.dll<br />php_pdo_sqlsrv_7_ts_x64.dll|7.0|是|64 位元 php7ts.dll|   

在 Linux 上，下列版本的驅動程式會包含：

|驅動程式檔案|PHP 版本|具備執行緒安全性？|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|否 |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|是|

**Microsoft Drivers 3.2 for PHP for SQL Server：**  

在 Windows 中，下列版本的驅動程式會包含：

|驅動程式檔案|PHP 版本|具備執行緒安全性？|與 PHP .dll 搭配使用|  
|---------------|:---------------:|:----------------:|---------------------|  
|php_sqlsrv_54_nts.dll<br />php_pdo_sqlsrv_54_nts.dll|5.4|否|php5.dll|  
|php_sqlsrv_54_ts.dll<br />php_pdo_sqlsrv_54_ts.dll|5.4|是|php5ts.dll|  
|php_sqlsrv_55_nts.dll<br />php_pdo_sqlsrv_55_nts.dll|5.5|否|php5.dll|  
|php_sqlsrv_55_ts.dll<br />php_pdo_sqlsrv_55_ts.dll|5.5|是|php5ts.dll|  
|php_sqlsrv_56_nts.dll<br />php_pdo_sqlsrv_56_nts.dll|5.6|否|php5.dll|  
|php_sqlsrv_56_ts.dll<br />php_pdo_sqlsrv_56_ts.dll|5.6|是|php5ts.dll|  

**Microsoft Drivers 3.1 for PHP for SQL Server：**  

在 Windows 中，下列版本的驅動程式會包含：

|驅動程式檔案|PHP 版本|具備執行緒安全性？|與 PHP .dll 搭配使用|  
|---------------|:---------------:|:----------------:|---------------------|  
|php_sqlsrv_54_nts.dll<br />php_pdo_sqlsrv_54_nts.dll|5.4|否|php5.dll|  
|php_sqlsrv_54_ts.dll<br />php_pdo_sqlsrv_54_ts.dll|5.4|是|php5ts.dll|  
|php_sqlsrv_55_nts.dll<br />php_pdo_sqlsrv_55_nts.dll|5.5|否|php5.dll|  
|php_sqlsrv_55_ts.dll<br />php_pdo_sqlsrv_55_ts.dll|5.5|是|php5ts.dll|  

## <a name="see-also"></a>另請參閱  
[開始使用 Microsoft Drivers for PHP for SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[適用於 SQL Server 程式設計適用於 PHP 的 Microsoft 驅動程式的指南](../../connect/php/programming-guide-for-php-sql-driver.md)

[SQLSRV 驅動程式 API 參考](../../connect/php/sqlsrv-driver-api-reference.md)

[PDO_SQLSRV 驅動程式 API 參考](../../connect/php/pdo-sqlsrv-driver-reference.md)  
