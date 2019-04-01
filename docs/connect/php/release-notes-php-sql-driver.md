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
manager: craigg
ms.openlocfilehash: 48c4497dfa8974fe5fd59747d4b7023002d3f762
ms.sourcegitcommit: c60784d1099875a865fd37af2fb9b0414a8c9550
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2019
ms.locfileid: "58646413"
---
# <a name="release-notes-for-the-microsoft-drivers-for-php-for-sql-server"></a>Microsoft Drivers for PHP for SQL Server 的版本資訊

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

此頁面說明每個版本中新增了哪些功能[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]。  

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

## <a name="whats-new-in-version-56"></a>5.6 版的新功能

| 新項目 | 詳細資料 |
| :------- | :------ |
| PHP 7.3 的支援。 | &nbsp; |
| 已卸除的對 PHP 7.0 的詳細資訊。 | &nbsp; |
| 所有平台上的 Microsoft ODBC 驅動程式 17.3 支援。 | &nbsp; |
| 適用於 macOS Mojave 的支援。 | 需要 17.3 的 ODBC 驅動程式或更新版本。 |
| 支援 Ubuntu 18.10 和 Suse Linux 15。 | 兩者都需要 ODBC 驅動程式 17.3 或更新版本。 |
| 卸除 Linux Ubuntu 17.10 和 El Capitan macOS 的支援。 | &nbsp; |
| Azure AD 存取權杖的支援。 | 在 Linux 和 macOS，需要有 ODBC 驅動程式 17.2 + 和 unixODBC 2.3.6+。 |
| 使用適用於 Azure 資源的受控身分識別與 Azure AD 的驗證支援。 | 需要 ODBC 驅動程式 17.3 +。 |
| 新的擷取功能 | &bull; &nbsp; 新的物件形式傳回日期時間的 pdo_sqlsrv PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE 旗標。<br/><br/>&bull; &nbsp; 加入陳述式層級 sqlsrv ReturnDatesAsStrings 選項。<br/><br/>&bull; &nbsp; 在這兩個驅動程式的格式擷取的結果中的十進位值的連接和陳述式層級的新選項。 |
| 如果使用者選擇要從來源建置的驅動程式的靜態編譯的支援。 | &nbsp; |
| 提升快取中繼資料的提取上，並加速 Unicode 字串轉換的效能。 | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="whats-new-in-version-53"></a>5.3 版的新功能

- 在所有平台上支援 Microsoft ODBC 驅動程式 17.2
- 支援使用 macOS High Sierra (需要 ODBC Driver 17 或以上版本)
- Azure 金鑰保存庫 Always Encrypted 的基本 CRUD 功能這類 Always Encrypted 功能是提供給所有支援 Windows、 Linux 或 macOS 平台[搭配 PHP Drivers for SQL Server 使用 Always Encrypted](../../connect/php/using-always-encrypted-php-drivers.md)
- 支援 Ubuntu 18.04 LTS （需要 ODBC 驅動程式 17.2）
- 在 Linux 或 macOS 也 （需要 ODBC 驅動程式 17.2） 中的連接恢復功能的支援

## <a name="whats-new-in-version-52"></a>5.2 版的新功能

- PHP 7.2.1 支援與更高層級上 Windows 和 7.2.0 與其他平台上的更高層級
- Microsoft ODBC driver 17 的支援
  - 第 17 版現在是在所有平台上的預設值
- 支援 Ubuntu 17.10、 Debian 9、 和 Suse Enterprise Linux 12
- 不再的支援 Ubuntu 15.10
- 在 Windows 上的 CRUD 功能 Always Encrypted 的支援。 如需詳細資訊，請參閱[搭配 PHP Drivers for SQL Server 使用 Always Encrypted](../../connect/php/using-always-encrypted-php-drivers.md)
  - 支援 Windows 憑證存放區
  - 一律加密僅適用於 Microsoft ODBC Driver 17 或更新版本
- 在 Linux 和 macOS 上的非 UTF8 地區設定支援
  - Microsoft ODBC Driver 17 或更新版本才支援在 Linux 和 macOS 上的非 UTF8 地區設定
- Azure SQL 資料倉儲的支援
- 支援 Azure SQL 受控執行個體 （延伸私人預覽）

## <a name="whats-new-in-version-43"></a>4.3 版的新功能

- PHP 7.1 的支援
- 支援使用 macOS Sierra 和 macOS El Capitan
- 支援的 Ubuntu 15.10 及 Debian 8
- Ubuntu 15.04 不再的支援
- Always On 可用性群組，透過透明網路 IP 解析支援。 如需詳細資訊，請參閱 [Connection Options](../../connect/php/connection-options.md)。
- 已新增的支援限制的 sql_variant 資料類型。
- 在 Windows 中的閒置連接恢復功能支援。 如需詳細資訊，請參閱 [Connection Options](../../connect/php/connection-options.md)。
- 連線集區 適用於 Linux 和 macOS 的支援。 如需詳細資訊，請參閱[連接共用](../../connect/php/connection-pooling-microsoft-drivers-for-php-for-sql-server.md)。
- 使用 ActiveDirectoryPassword 和 SqlPassword 的 Azure Active Directory 驗證支援。 如需詳細資訊，請參閱 [Connection Options](../../connect/php/connection-options.md)。

## <a name="whats-new-in-version-40"></a>4.0 版的新功能

- PHP 7.0 的支援  
- 完整的 64 位元支援
- Ubuntu 15.04、 Ubuntu 16.04 和 RedHat 7 支援

## <a name="whats-new-in-version-32"></a>3.2 版的新功能

- PHP 5.6 的支援   
- 包含 PHP 舊有的 5.5 和 5.4 版最新的更新   
- 需要 Microsoft ODBC Driver 11 for SQL Server  

## <a name="whats-new-in-version-31"></a>3.1 版的新功能

- PHP 5.5 的支援  
- 需要 Microsoft ODBC Driver 11 for SQL Server。 舊版需要 SQL Native Client。  

## <a name="whats-new-in-version-30"></a>3.0 版的新功能  

- PHP 5.4 的支援  [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]第 3 版不支援 PHP 5.2。  
- 已加入 AttachDBFileName 連接選項。 如需詳細資訊，請參閱 [Connection Options](../../connect/php/connection-options.md)。  
- LocalDB 的支援，已在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中新增。 如需詳細資訊，請參閱 < [LocalDB 的支援](../../connect/php/php-driver-for-sql-server-support-for-localdb.md)。
- 已加入 AttachDBFileName 連接選項。 如需詳細資訊，請參閱 [Connection Options](../../connect/php/connection-options.md)。  
- 高可用性與災害復原功能的支援。 如需詳細資訊，請參閱 <<c0> [ 支援高可用性、 災害復原](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)。
- 用戶端資料指標的支援 (快取記憶體中的結果集)。 如需詳細資訊，請參閱[資料指標類型 &#40;SQLSRV 驅動程式&#41;](../../connect/php/cursor-types-sqlsrv-driver.md) 和[資料指標類型 &#40;PDO_SQLSRV 驅動程式&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)。
- 已加入 PDO::ATTR_EMULATE_PREPARES 屬性。 如需詳細資訊，請參閱 [PDO::prepare](../../connect/php/pdo-prepare.md)。  

## <a name="whats-new-in-version-20"></a>2.0 版的新功能

在 2.0 版中，已加入對 PDO_SQLSRV 驅動程式的支援。 如需詳細資訊，請參閱 [PDO_SQLSRV 驅動程式參考](../../connect/php/pdo-sqlsrv-driver-reference.md)。  

## <a name="see-also"></a>另請參閱

[Microsoft Drivers for PHP for SQL Server 概觀](../../connect/php/overview-of-the-php-sql-driver.md)
