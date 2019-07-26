---
title: Microsoft Drivers for PHP for SQL Server 的版本資訊 | Microsoft Docs
ms.custom: ''
ms.date: 02/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: v-dapugl, kenvh
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- what's new in version 1.1
ms.assetid: 91cca3d2-ba99-4a6d-b0de-beb9699cb3f8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 23ac53a8515f55dfc0cad282fd14294e5f285af9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67935910"
---
# <a name="release-notes-for-the-microsoft-drivers-for-php-for-sql-server"></a>Microsoft Drivers for PHP for SQL Server 的版本資訊

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

此頁面會討論每個版本[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]中新增的內容。  

<!--
Hello, We are standardizing the format of content inside our Release Notes (or What's New) articles.
Instead of bullets (or paragraphs), we have shifted to the 2-column format you see for H2 **What's New in Version 5.6**.
It is not necessary to reformat all the older H2 sections in this Release Notes file, but.....

Going forward, please be sure to use the 2-column format.

Also, all Release Notes .md file names now must begin with 'release-notes-*.md'.  And no filler words.
The 5.6 edition of this file is being renamed.....
FROM:  'release-notes-for-the-php-sql-driver.md'
TO  :  'release-notes-php-sql-driver.md'

For any questions, ask GeneMi or CraigG.
Thanks a lot.  2019-03-28  (DevO= 1467988)
-->

## <a name="whats-new-in-version-56"></a>5\.6 版的新功能

| 新項目 | 詳細資料 |
| :------- | :------ |
| PHP 7.3 的支援。 | &nbsp; |
| 已捨棄對 PHP 7.0 的支援。 | &nbsp; |
| 所有平臺上的 Microsoft ODBC Driver 17.3 支援。 | &nbsp; |
| 支援 macOS Mojave。 | 需要 ODBC 驅動程式17.3 或更新版本。 |
| Ubuntu 18.10 和 Suse Linux 15 的支援。 | 兩者都需要 ODBC 驅動程式17.3 或更新版本。 |
| 已捨棄 Linux Ubuntu 17.10 和 macOS El Capitan 的支援。 | &nbsp; |
| 支援 Azure AD 存取權杖。 | 在 Linux 和 macOS 中, 需要 ODBC 驅動程式 17.2 + 和 unixODBC 2.3.6 +。 |
| 支援使用 Azure 資源的受控識別, 透過 Azure AD 進行驗證。 | 需要 ODBC 驅動程式 17.3 +。 |
| 新的 fetch 功能 | &bull;&nbsp;適用于 pdo_sqlsrv 的新 PDO:: SQLSRV_ATTR_FETCHES_DATETIME_TYPE 旗標, 會以物件的形式傳回 DATETIME。<br/><br/>&bull;&nbsp;將 ReturnDatesAsStrings 選項加入至 sqlsrv 的語句層級。<br/><br/>&bull;&nbsp;連接和語句層級的新選項, 適用于將提取結果中的十進位值格式化的驅動程式。 |
| 如果使用者選擇從來源建立, 則支援驅動程式的靜態編譯。 | &nbsp; |
| 藉由快取提取和加速 Unicode 字串轉換的中繼資料來改善效能。 | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="whats-new-in-version-53"></a>5\.3 版的新功能

- 支援所有平臺上的 Microsoft ODBC Driver 17。2
- MacOS High 的支援 (需要 ODBC Driver 17 和更新版本)
- 支援基本 CRUD 功能 Always Encrypted 的 Azure Key Vault, 因此 Always Encrypted 功能適用于所有支援的 Windows、Linux 或 macOS 平臺, 並搭配[PHP 驅動程式 for SQL Server 使用 Always Encrypted](../../connect/php/using-always-encrypted-php-drivers.md)
- 支援 Ubuntu 18.04 LTS (需要 ODBC 驅動程式 17.2)
- 同時支援 Linux 或 macOS 中的連接恢復功能 (需要 ODBC 驅動程式 17.2)

## <a name="whats-new-in-version-52"></a>5\.2 版的新功能

- 支援在 Windows 上進行 PHP 7.2.1 和更新, 以及在其他平臺上7.2.0 和啟動
- Microsoft ODBC Driver 17 的支援
  - 17版現在是所有平臺上的預設值
- 支援 Ubuntu 17.10、Debian 9 和 Suse Enterprise Linux 12
- 已捨棄 Ubuntu 15.10 的支援
- 支援在 Windows 上使用 CRUD 功能 Always Encrypted。 如需詳細資訊，請參閱[搭配 PHP Drivers for SQL Server 使用 Always Encrypted](../../connect/php/using-always-encrypted-php-drivers.md)
  - 支援 Windows 憑證存放區
  - 只有 Microsoft ODBC Driver 17 和更新版本才支援 Always Encrypted
- Linux 和 macOS 上的非 UTF8 地區設定支援
  - Linux 和 macOS 上的非 UTF8 地區設定僅支援 Microsoft ODBC Driver 17 和更新版本
- Azure SQL 資料倉儲的支援
- 對 Azure SQL 受控執行個體 (延伸個人預覽版) 的支援

## <a name="whats-new-in-version-43"></a>4\.3 版的新功能

- PHP 7.1 的支援
- 支援 macOS Sierra 和 macOS El Capitan
- 支援 Ubuntu 15.10 和 Debian 8
- 已捨棄 Ubuntu 15.04 的支援
- 透過透明的網路 IP 解析支援 Always On 可用性群組。 如需詳細資訊，請參閱 [Connection Options](../../connect/php/connection-options.md)。
- 已新增對 SQL_variant 資料類型的支援, 但有限制。
- Windows 中的閒置連接恢復功能支援。 如需詳細資訊，請參閱 [Connection Options](../../connect/php/connection-options.md)。
- Linux 和 macOS 的連接共用支援。 如需詳細資訊，請參閱[連接共用](../../connect/php/connection-pooling-microsoft-drivers-for-php-for-sql-server.md)。
- 支援使用 ActiveDirectoryPassword 和 SqlPassword 進行 Azure Active Directory 驗證。 如需詳細資訊，請參閱 [Connection Options](../../connect/php/connection-options.md)。

## <a name="whats-new-in-version-40"></a>4\.0 版的新功能

- PHP 7.0 的支援  
- 完整64位支援
- 支援 Ubuntu 15.04、Ubuntu 16.04 和 RedHat 7

## <a name="whats-new-in-version-32"></a>3\.2 版的新功能

- PHP 5.6 的支援   
- 包含 PHP 舊有的 5.5 和 5.4 版最新的更新   
- 需要 Microsoft ODBC Driver 11 for SQL Server  

## <a name="whats-new-in-version-31"></a>3\.1 版的新功能

- PHP 5.5 的支援  
- 需要 Microsoft ODBC Driver 11 for SQL Server。 舊版需要 SQL Native Client。  

## <a name="whats-new-in-version-30"></a>3\.0 版的新功能  

- PHP 5.4 的支援  [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]第 3 版不支援 PHP 5.2。  
- 已加入 AttachDBFileName 連接選項。 如需詳細資訊，請參閱 [Connection Options](../../connect/php/connection-options.md)。  
- LocalDB 的支援，已在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中新增。 如需詳細資訊，請參閱[支援 LocalDB](../../connect/php/php-driver-for-sql-server-support-for-localdb.md)。
- 已加入 AttachDBFileName 連接選項。 如需詳細資訊，請參閱 [Connection Options](../../connect/php/connection-options.md)。  
- 高可用性與災害復原功能的支援。 如需詳細資訊，請參閱[對於高可用性、災害復原的支援](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)。
- 用戶端資料指標的支援 (快取記憶體中的結果集)。 如需詳細資訊，請參閱[資料指標類型 &#40;SQLSRV 驅動程式&#41;](../../connect/php/cursor-types-sqlsrv-driver.md) 和[資料指標類型 &#40;PDO_SQLSRV 驅動程式&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)。
- 已加入 PDO::ATTR_EMULATE_PREPARES 屬性。 如需詳細資訊，請參閱 [PDO::prepare](../../connect/php/pdo-prepare.md)。  

## <a name="whats-new-in-version-20"></a>2\.0 版的新功能

在 2.0 版中，已加入對 PDO_SQLSRV 驅動程式的支援。 如需詳細資訊，請參閱 [PDO_SQLSRV 驅動程式參考](../../connect/php/pdo-sqlsrv-driver-reference.md)。  

## <a name="see-also"></a>另請參閱

[Microsoft Drivers for PHP for SQL Server 概觀](../../connect/php/overview-of-the-php-sql-driver.md)
