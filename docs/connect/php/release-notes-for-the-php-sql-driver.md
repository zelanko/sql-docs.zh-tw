---
title: "PHP SQL 驅動程式的版本資訊 |Microsoft 文件"
ms.custom: 
ms.date: 07/12/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- what's new in version 1.1
ms.assetid: 91cca3d2-ba99-4a6d-b0de-beb9699cb3f8
caps.latest.revision: 37
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2c63079bda91844995540aade94bac397be6b94c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="release-notes-for-the-php-sql-driver"></a>PHP SQL 驅動程式的版本資訊
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本主題將討論每個版本中加入的項目[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]。  

## <a name="whats-new-in-version-43"></a>4.3 版中最新消息

- PHP 7.1 的支援
- Mac OS 利也和 Mac OS El Capitan 支援
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
- LocalDB 的支援，已在 [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]中加入。 如需詳細資訊，請參閱 [PHP Driver for SQL Server Support for LocalDB](../../connect/php/php-driver-for-sql-server-support-for-localdb.md)。
- 已加入 AttachDBFileName 連接選項。 如需詳細資訊，請參閱 [Connection Options](../../connect/php/connection-options.md)。  
- 高可用性與災害復原功能的支援。 如需詳細資訊，請參閱 [PHP Driver for SQL Server 對於高可用性、災害復原的支援](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)。
- 用戶端資料指標的支援 (快取記憶體中的結果集)。 如需詳細資訊，請參閱[資料指標類型 &#40;SQLSRV 驅動程式 &#41;](../../connect/php/cursor-types-sqlsrv-driver.md)和[資料指標類型 &#40;PDO_SQLSRV 驅動程式 &#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md).
- 已加入 PDO::ATTR_EMULATE_PREPARES 屬性。 如需詳細資訊，請參閱[pdo:: prepare](../../connect/php/pdo-prepare.md)。  
  
## <a name="whats-new-in-version-20"></a>2.0 版的新功能  
在 2.0 版中，已加入對 PDO_SQLSRV 驅動程式的支援。 如需詳細資訊，請參閱 [PDO_SQLSRV 驅動程式參考](../../connect/php/pdo-sqlsrv-driver-reference.md)。  
  
## <a name="see-also"></a>另請參閱  
[PHP SQL 驅動程式概觀](../../connect/php/overview-of-the-php-sql-driver.md)
  

