---
title: "PHP SQL 驅動程式的系統需求 |Microsoft 文件"
ms.custom: 
ms.date: 07/12/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: requirements
ms.assetid: 5db4b75f-c605-4785-9560-399a533c0fc9
caps.latest.revision: "93"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: abff6843dbf1b8f1362f10dbf2fe52fa5f686515
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="system-requirements-for-the-php-sql-driver"></a>PHP SQL 驅動程式的系統需求
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

將存取資料的 SQL Server 或 Azure SQL Database 使用[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]，您必須擁有您電腦上安裝下列元件：  
  
-   PHP 是必要的。 如需如何下載並安裝最新的穩定二進位檔的資訊，請參閱[http://php.net](http://go.microsoft.com/fwlink/?LinkId=101876)。  Microsoft Drivers for PHP for SQL Server 需要下列版本：
  
|Microsoft Drivers for PHP for SQL Server 版本|支援的 PHP 版本|  
|----------------------------------------------------|--------------------------|  
|4.3|PHP 7.0 和 PHP 7.1| 
|4.0|PHP 7.0|  
|3.2|PHP 5.6.4+ 或<br /><br />PHP 5.5.16+ 或<br /><br />PHP 5.4.32|  
|3.1|PHP 5.5.16+ 或<br /><br />PHP 5.4.32|  
|3.0|PHP 5.4.32 或<br /><br />PHP 5.3.0|  
|2.0|PHP 5.3.0 或<br /><br />PHP 5.2.4 或<br /><br />PHP 5.2.13|  
  
-   您的 PHP 延伸目錄中必須要有某個版本的驅動程式檔案。 如需不同驅動程式檔案的相關資訊，請參閱本主題稍後的「驅動程式版本」。 如需為 PHP 執行階段設定驅動程式的資訊，請參閱 [載入 PHP SQL 驅動程式](../../connect/php/loading-the-php-sql-driver.md)  。 若要載入驅動程式，請參閱 [Microsoft Drivers for PHP for SQL Server](http://www.microsoft.com/download/details.aspx?id=20098)。  
  
-   需要 Web 伺服器。 您的 Web 伺服器必須設定為執行 PHP。 如需裝載 PHP 應用程式的網際網路資訊服務 (IIS) 6.0 與資訊，請參閱[使用 FastCGI 在 IIS 6.0 上裝載 PHP 應用程式](http://go.microsoft.com/fwlink/?LinkId=117131)。 如需透過 IIS 7.0 裝載 PHP 應用程式的相關資訊，請參閱 [使用 FastCGI 在 IIS 7.0 上裝載 PHP 應用程式](http://go.microsoft.com/fwlink/?LinkId=117132)。  
  
    [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 經過使用 FastCGI 的 IIS 6 和 IIS 7 的測試。  
  
    > [!NOTE]  
    > Microsoft 僅提供 IIS 的支援。  
  
-   PHP 執行所在的電腦上需要 Microsoft ODBC Driver for SQL Server 或 SQL Server Native Client 的正確版本。  如果您使用 64 位元作業系統，ODBC 64 位元安裝程式會安裝 32 位元和 64 位元 ODBC 驅動程式。 如果您使用 32 位元作業系統，請使用 ODBC x86 安裝程式。

|Microsoft Drivers for PHP for SQL Server 版本|版本的 Microsoft ODBC Driver for SQL Server 或 SQL Server Native Client|  
|----------------------------------------------------|--------------------------|
|4.3|Microsoft ODBC Driver 11 for SQL Server 或 Microsoft ODBC Driver 13.1 for SQL Server。 若要下載 Microsoft ODBC 驅動程式，請參閱[Microsoft ODBC Driver 11 for SQL Server 頁面](http://www.microsoft.com/download/details.aspx?id=36434)或[Microsoft ODBC Driver 13.1 for SQL Server 頁面](https://www.microsoft.com/en-us/download/details.aspx?id=53339)|    
|4.0|Microsoft ODBC Driver 11 for SQL Server 或 Microsoft ODBC Driver 13 for SQL Server。 若要下載 Microsoft ODBC 驅動程式，請參閱[Microsoft ODBC Driver 11 for SQL Server 頁面](http://www.microsoft.com/download/details.aspx?id=36434)或[Microsoft ODBC Driver 13 for SQL Server 頁面](https://www.microsoft.com/download/details.aspx?id=50420)|  
|3.2 或 <br><br> 3.1|Microsoft ODBC Driver 11 for SQL Server。 若要下載 Microsoft ODBC 驅動程式，請參閱[Microsoft ODBC Driver 11 for SQL Server 頁面](http://www.microsoft.com/download/details.aspx?id=36434)|   
|3.0|Microsoft [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] Native Client。 您可以從 [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] SQL Server 2012 功能套件頁面 [下載 Microsoft](http://go.microsoft.com/fwlink/?LinkID=236805)| 
|2.0|Microsoft[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro_md.md)]原生用戶端：<br /><br />[下載 X86 封裝](http://go.microsoft.com/fwlink/?LinkID=188400&clcid=0x409)32 位元作業系統 <br /><br />[下載 X64 封裝](http://go.microsoft.com/fwlink/?LinkID=188401&clcid=0x409)64 位元作業系統|  

  
如果您使用 SQLSRV 驅動程式[sqlsrv_client_info](../../connect/php/sqlsrv-client-info.md)傳回哪個版本的相關資訊[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]原生用戶端或 Microsoft ODBC Driver for SQL Server 正在使用[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]。 如果您使用 PDO_SQLSRV 驅動程式，您可以使用[pdo:: getattribute](../../connect/php/pdo-getattribute.md)來探索版本。  



## <a name="database-versions"></a>資料庫版本
-   支援 azure SQL 資料庫。 如需資訊，請參閱[連接到 Microsoft Azure SQL Database](../../connect/php/connecting-to-microsoft-azure-sql-database.md)。 

- [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]4.3 支援 SQL Server 2008 R2 的版本和更新版本
- [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]4.0 版支援 SQL Server 2008 及更新版本
- [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]3.1 版支援 SQL Server 2008 及更新版本
- [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]版本 2.0 和 3.0 支援 SQL Server 2005 和更新版本


## <a name="driver-versions"></a>驅動程式版本  
此區段會列出所包含的每個版本的驅動程式[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]。  
  
若要設定使用的驅動程式，PHP 執行階段，請依照下列中的安裝指示[載入 PHP SQL 驅動程式](../../connect/php/loading-the-php-sql-driver.md)。  
  
**Microsoft Drivers 4.3 for PHP for SQL Server:**  

在 Windows 中，為 4.3 下列版本的驅動程式會安裝：
  
|驅動程式檔案|PHP 版本|具備執行緒安全性？|與 PHP .dll 搭配使用|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_7_nts_x86.dll<br /><br />php_pdo_sqlsrv_7_nts_x86.dll|7.0|否|32 位元 php7.dll| 
|php_sqlsrv_7_ts_x86.dll<br /><br />php_pdo_sqlsrv_7_ts_x86.dll|7.0|是|32 位元 php7ts.dll| 
|php_sqlsrv_7_nts_x64.dll<br /><br />php_pdo_sqlsrv_7_nts_x64.dll|7.0|否|64 位元 php7.dll|  
|php_sqlsrv_7_ts_x64.dll<br /><br />php_pdo_sqlsrv_7_ts_x64.dll|7.0|是|64 位元 php7ts.dll| 
|php_sqlsrv_71_nts_x86.dll<br /><br />php_pdo_sqlsrv_71_nts_x86.dll|7.1|否|32 位元 php7.dll|  
|php_sqlsrv_71_ts_x86.dll<br /><br />php_pdo_sqlsrv_71_ts_x86.dll|7.1|是|32 位元 php7ts.dll|  
|php_sqlsrv_71_nts_x64.dll<br /><br />php_pdo_sqlsrv_71_nts_x64.dll|7.1|否|64 位元 php7.dll|  
|php_sqlsrv_71_ts_x64.dll<br /><br />php_pdo_sqlsrv_71_ts_x64.dll|7.1|是|64 位元 php7ts.dll|   
  
**Microsoft Driver 4.0 for PHP for SQL Server:**  

在 Windows 中，針對 4.0 下列版本的驅動程式會安裝：
  
|驅動程式檔案|PHP 版本|具備執行緒安全性？|與 PHP .dll 搭配使用|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_7_nts_x86.dll<br /><br />php_pdo_sqlsrv_7_nts_x86.dll|7.0|否|32 位元 php7.dll|  
|php_sqlsrv_7_ts_x86.dll<br /><br />php_pdo_sqlsrv_7_ts_x86.dll|7.0|是|32 位元 php7ts.dll|  
|php_sqlsrv_7_nts_x64.dll<br /><br />php_pdo_sqlsrv_7_nts_x64.dll|7.0|否|64 位元 php7.dll|  
|php_sqlsrv_7_ts_x64.dll<br /><br />php_pdo_sqlsrv_7_ts_x64.dll|7.0|是|64 位元 php7ts.dll|   
  
支援的 Linux 版本中，sqlsrv 和/或 pdo_sqlsrv 的適當版本可以使用 PHP 的 PECL 封裝系統安裝。 
  
**Microsoft Drivers 3.2 for PHP for SQL Server 會安裝下列版本的驅動程式：**  
  
|驅動程式檔案|PHP 版本|具備執行緒安全性？|與 PHP .dll 搭配使用|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_54_nts.dll<br /><br />php_pdo_sqlsrv_54_nts.dll|5.4|否|php5.dll|  
|php_sqlsrv_54_ts.dll<br /><br />php_pdo_sqlsrv_54_ts.dll|5.4|是|php5ts.dll|  
|php_sqlsrv_55_nts.dll<br /><br />php_pdo_sqlsrv_55_nts.dll|5.5|否|php5.dll|  
|php_sqlsrv_55_ts.dll<br /><br />php_pdo_sqlsrv_55_ts.dll|5.5|是|php5ts.dll|  
|php_sqlsrv_56_nts.dll<br /><br />php_pdo_sqlsrv_56_nts.dll|5.6|否|php5.dll|  
|php_sqlsrv_56_ts.dll<br /><br />php_pdo_sqlsrv_56_ts.dll|5.6|是|php5ts.dll|  
  
**Microsoft Drivers 3.1 for PHP for SQL Server 會安裝下列版本的驅動程式：**  
  
|驅動程式檔案|PHP 版本|具備執行緒安全性？|與 PHP .dll 搭配使用|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_54_nts.dll<br /><br />php_pdo_sqlsrv_54_nts.dll|5.4|否|php5.dll|  
|php_sqlsrv_54_ts.dll<br /><br />php_pdo_sqlsrv_54_ts.dll|5.4|是|php5ts.dll|  
|php_sqlsrv_55_nts.dll<br /><br />php_pdo_sqlsrv_55_nts.dll|5.5|否|php5.dll|  
|php_sqlsrv_55_ts.dll<br /><br />php_pdo_sqlsrv_55_ts.dll|5.5|是|php5ts.dll|  
  
**Microsoft Drivers 3.0 for PHP for SQL Server 會安裝下列版本的驅動程式：**  
  
|驅動程式檔案|PHP 版本|具備執行緒安全性？|與 PHP .dll 搭配使用|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_53_nts.dll<br /><br />php_pdo_sqlsrv_53_nts.dll|5.3|否|php5.dll|  
|php_sqlsrv_53_ts.dll<br /><br />php_pdo_sqlsrv_53_ts.dll|5.3|是|php5ts.dll|  
|php_sqlsrv_54_nts.dll<br /><br />php_pdo_sqlsrv_54_nts.dll|5.4|否|php5.dll|  
|php_sqlsrv_54_ts.dll<br /><br />php_pdo_sqlsrv_54_ts.dll|5.4|是|php5ts.dll|  
  
**Microsoft Drivers 2.0 for PHP for SQL Server 會安裝下列版本的驅動程式：**  
  
|驅動程式檔案|PHP 版本|具備執行緒安全性？|與 PHP .dll 搭配使用|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_53_nts_vc6.dll<br /><br />php_pdo_sqlsrv_53_nts_vc6.dll|5.3|否|php5.dll|  
|php_sqlsrv_53_nts_vc9.dll<br /><br />php_pdo_sqlsrv_53_nts_vc9.dll|5.3|否|php5.dll|  
|php_sqlsrv_53_ts_vc6.dll<br /><br />php_pdo_sqlsrv_53_ts_vc6.dll|5.3|是|php5ts.dll|  
|php_sqlsrv_53_ts_vc9.dll<br /><br />php_pdo_sqlsrv_53_ts_vc9.dll|5.3|是|php5ts.dll|  
|php_sqlsrv_52_nts_vc6.dll<br /><br />php_pdo_sqlsrv_52_nts_vc6.dll|5.2|否|php5.dll|  
|php_sqlsrv_52_ts_vc6.dll<br /><br />php_pdo_sqlsrv_52_ts_vc6.dll|5.2|是|php5ts.dll|  
  
如果驅動程式檔案的名稱包含 "vc9"，則應該用於使用 Visual C++ 9.0 進行編譯的 PHP 版本。  
## <a name="operating-systems"></a>作業系統 
以下是支援的作業系統版本的驅動程式：

-   4.3:
    -   Windows Server 2012  
    -   Windows Server 2012 R2
    -   Windows Server 2016 
    -   Windows 8  
    -   Windows 8.1   
    -   Windows 10
    -   Ubuntu 15.10 （64 位元）
    -   Ubuntu 16.04 （64 位元）
    -   Debian 8 （64 位元）
    -   Red Hat Enterprise Linux 7 （64 位元）
    -   Mac OS 利也 （64 位元）
    -   Mac OS El Capitan （64 位元）
    
-   4.0:  
    -   Windows Server 2008 SP2
    -   Windows Server 2008 R2 SP1  
    -   Windows Server 2012  
    -   Windows Server 2012 R2  
    -   Windows Vista SP2  
    -   Windows 7 SP1  
    -   Windows 8  
    -   Windows 8.1   
    -   Windows 10 
    -   Ubuntu 15.04 （64 位元）
    -   Ubuntu 16.04 （64 位元）
    -   Red Hat Enterprise Linux 7 （64 位元）

 
-   3.2 和 3.1 版：  
    -   Windows Server 2008 R2 SP1  
    -   Windows Vista SP2  
    -   Windows Server 2008 SP2  
    -   Windows 7 SP1  
    -   Windows Server 2012  
    -   Windows Server 2012 R2  
    -   Windows 8  
    -   Windows 8.1  
  
  
-   3.0:  
    -   Windows Server 2008 R2 SP1  
    -   Windows Vista SP2  
    -   Windows Server 2008 SP2  
    -   Windows 7 SP1  


-   2.0:
    -   [!INCLUDE[winxpsvr](../../includes/winxpsvr_md.md)] Service Pack 1  
    -   Windows XP Service Pack 3  
    -   Windows Vista Service Pack 1 或更新版本  
    -   Windows Server 2008  
    -   Windows Server 2008 R2  
    -   Windows 7  
  
## <a name="see-also"></a>另請參閱  
[PHP SQL 驅動程式快速入門](../../connect/php/getting-started-with-the-php-sql-driver.md)
[PHP SQL 驅動程式程式設計指南](../../connect/php/programming-guide-for-php-sql-driver.md)
[SQLSRV 驅動程式 API 參考](../../connect/php/sqlsrv-driver-api-reference.md)  
  
