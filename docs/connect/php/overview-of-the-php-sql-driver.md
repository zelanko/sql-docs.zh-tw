---
title: Microsoft Drivers for PHP for SQL Server 概觀 | Microsoft Docs
ms.custom: ''
ms.date: 03/27/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 66559249-34c0-409d-b919-9b5bf0c4c9ec
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 25519d06df8b948d5cfc5d387029cf09beafc856
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936278"
---
# <a name="overview-of-the-microsoft-drivers-for-php-for-sql-server"></a>Microsoft Drivers for PHP for SQL Server 概觀

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 是一個 PHP 延伸模組，可提供對 SQL Server 2005 和更新版本 (包括 Azure SQL Database) 的資料存取。 此延伸模組提供程式性介面與 SQLSRV 驅動程式, 以及具有 PDO_SQLSRV 驅動程式的物件導向介面, 可用來存取所有版本 SQL Server 中的資料, 包括 Express, 從 SQL Server 2005 開始。 3\.1 和更新版本的驅動程式支援從 SQL Server 2008 開始。 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] API 包含對 Windows 驗證、交易、參數繫結、資料流、中繼資料存取和錯誤處理的支援。  
  
若要使用[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], 您必須將正確的 SQL Server Native Client 或 Microsoft ODBC 驅動程式版本安裝在 PHP 執行所在的同一部電腦上。  如需詳細資訊, 請參閱[適用于 PHP 的 Microsoft 驅動程式的系統需求 SQL Server](../../connect/php/system-requirements-for-the-php-sql-driver.md)。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|Description|  
|---------|---------------|  
| ![下載-Download-downarrow-circled](../../ssdt/media/download.png)[以下載 PHP 的驅動程式, 以供 SQL Server](download-drivers-php-sql-server.md) | 下載 Microsoft Drivers for PHP for SQL Server 的連結。 |
|[Microsoft Drivers for PHP for SQL Server 的版本資訊](../../connect/php/release-notes-php-sql-driver.md)|列出 4.0、3.2、3.1、3.0 和 2.0 版已新增的功能。|  
|[Microsoft Drivers for PHP for SQL Server 的支援資源](../../connect/php/support-resources-for-the-php-sql-driver.md)|提供可在您開發使用 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的應用程式時提供協助的資源連結。|  
|[關於文件中的程式碼範例](../../connect/php/about-code-examples-in-the-documentation.md)|提供可在您執行此文件中的程式碼範例時很有幫助的資訊。|  
| &nbsp; | &nbsp; |

## <a name="reference"></a>參考

[SQLSRV 驅動程式 API 參考](../../connect/php/sqlsrv-driver-api-reference.md)  
[PDO_SQLSRV 驅動程式參考](../../connect/php/pdo-sqlsrv-driver-reference.md)  
[常數 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  

## <a name="see-also"></a>另請參閱

[開始使用 Microsoft Drivers for PHP for SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Microsoft Drivers for PHP for SQL Server 的程式設計指南](../../connect/php/programming-guide-for-php-sql-driver.md)

[範例應用程式 &#40;SQLSRV 驅動程式&#41;](../../connect/php/example-application-sqlsrv-driver.md)
