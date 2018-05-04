---
title: 版本資訊 Microsoft Drivers for PHP for SQL Server |Microsoft 文件
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- what's new in version 1.1
ms.assetid: 91cca3d2-ba99-4a6d-b0de-beb9699cb3f8
caps.latest.revision: 37
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 54d96ad2976d962e4828f9a5fd43fb81ee49f148
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="release-notes-for-the-microsoft-drivers-for-php-for-sql-server"></a>Microsoft Drivers for PHP for SQL Server 的版本資訊
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

此頁面會討論每個版本中加入的項目[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]。  

## <a name="whats-new-in-version-52"></a>5.2 版中最新消息

- PHP 7.2.1 支援 Windows 和 7.2.0 上最多和其他平台上的向上
- Microsoft ODBC driver 17 的支援
  - 已在所有平台上的預設版本 17。
- Ubuntu 17.10、 Debian 9、 和 Suse Enterprise Linux 12 的支援
- 不再的支援 Ubuntu 15.10
- 在 Windows 上的 CRUD 原有的一律加密支援。 如需詳細資訊，請參閱[Using Always Encrypted with SQL Server 的 PHP 驅動程式](../../connect/php/using-always-encrypted-php-drivers.md)
  - 支援 Windows 憑證存放區
  - 一律加密僅適用於 Microsoft ODBC 驅動程式 17 或更新版本
- Linux 及 macOS 非 UTF8 地區設定支援
  - Microsoft ODBC 驅動程式 17 或更新版本才支援在 Linux 和 macOS 非 UTF8 地區設定
- Azure SQL 資料倉儲的支援
- 支援 SQL Azure 受管理的執行個體 （擴充私人預覽中）


## <a name="whats-new-in-version-43"></a>4.3 版中最新消息

- PHP 7.1 的支援
- MacOS 利也支援及 macOS El Capitan
- Ubuntu 15.10 和 Debian 8 的支援
- Ubuntu 15.04 不再的支援
- 支援 Alwayson 可用性群組，透過透明網路 IP 解析。 如需詳細資訊，請參閱 [Connection Options](../../connect/php/connection-options.md)。
- 已新增的支援限制的 sql_variant 資料類型。
- 在 Windows 中的閒置連接恢復功能支援。 如需詳細資訊，請參閱 [Connection Options](../../connect/php/connection-options.md)。
- 連接共用支援的 Linux 及 macOS。 如需詳細資訊，請參閱[連接共用](../../connect/php/connection-pooling-microsoft-drivers-for-php-for-sql-server.md)。
- SqlPassword ActiveDirectoryPassword 與 Azure Active Directory 驗證的支援。 如需詳細資訊，請參閱 [Connection Options](../../connect/php/connection-options.md)。

## <a name="whats-new-in-version-40"></a>4.0 版中最新消息

- PHP 7.0 支援  
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
- LocalDB 的支援，已在 [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]中加入。 如需詳細資訊，請參閱[LocalDB 的支援](../../connect/php/php-driver-for-sql-server-support-for-localdb.md)。
- 已加入 AttachDBFileName 連接選項。 如需詳細資訊，請參閱 [Connection Options](../../connect/php/connection-options.md)。  
- 高可用性與災害復原功能的支援。 如需詳細資訊，請參閱[Support for High Availability，Disaster Recovery](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)。
- 用戶端資料指標的支援 (快取記憶體中的結果集)。 如需詳細資訊，請參閱[資料指標類型&#40;SQLSRV 驅動程式&#41;](../../connect/php/cursor-types-sqlsrv-driver.md)和[資料指標類型&#40;PDO_SQLSRV 驅動程式&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)。
- 已加入 PDO::ATTR_EMULATE_PREPARES 屬性。 如需詳細資訊，請參閱[pdo:: prepare](../../connect/php/pdo-prepare.md)。  

## <a name="whats-new-in-version-20"></a>2.0 版的新功能  
在 2.0 版中，已加入對 PDO_SQLSRV 驅動程式的支援。 如需詳細資訊，請參閱 [PDO_SQLSRV 驅動程式參考](../../connect/php/pdo-sqlsrv-driver-reference.md)。  

## <a name="see-also"></a>另請參閱  
[Microsoft Drivers for PHP for SQL Server 的概觀](../../connect/php/overview-of-the-php-sql-driver.md)
