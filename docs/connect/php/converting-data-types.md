---
title: 轉換資料類型 |Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 508542ec-cc28-4a17-80f4-52325d6a48db
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ca79a13146df59b0c7159de112feee3ec478249d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015104"
---
# <a name="converting-data-types"></a>轉換資料類型
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 可讓您指定當您將資料傳送至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或從中擷取資料時的資料類型。 指定資料類型是選擇性的。 如果未指定資料類型，則會使用預設類型。 本節中的主題將說明如何指定資料類型，並提供預設資料類型的詳細資料。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|Description|  
|---------|---------------|  
|[預設 SQL Server 資料類型](../../connect/php/default-sql-server-data-types.md)|提供將資料傳送至伺服器時的預設 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型的相關資訊。|  
|[預設 PHP 資料類型](../../connect/php/default-php-data-types.md)|提供從伺服器擷取資料時的預設 PHP 資料類型的相關資訊。|  
|[如何：指定 SQL Server 資料類型](../../connect/php/how-to-specify-sql-server-data-types-when-using-the-sqlsrv-driver.md)|示範如何指定將資料傳送至伺服器時的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型。|  
|[如何：指定 PHP 資料類型](../../connect/php/how-to-specify-php-data-types.md)|示範如何指定從伺服器擷取資料時的 PHP 資料類型。|  
|[如何：使用內建的 UTF-8 支援傳送及擷取 UTF-8 資料](../../connect/php/how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support.md)|示範如何使用 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 對於 UTF-8 資料的內建支援。<br /><br />[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 1.1 版已新增 UTF-8 字元的支援。|  
|[如何：傳送及擷取 Linux 與 macOS 中的 ASCII 資料](../../connect/php/how-to-send-and-retrieve-ascii-data-in-linux-mac.md)|示範如何在 Linux [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]或 macOS 中使用 ASCII 資料的支援。<br /><br />5\.2 版中已加入非 Windows 環境中的 ASCII 字元支援[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]。|
  
## <a name="see-also"></a>另請參閱  
[Microsoft Drivers for PHP for SQL Server 的程式設計指南](../../connect/php/programming-guide-for-php-sql-driver.md)

[SQLSRV 驅動程式 API 參考](../../connect/php/sqlsrv-driver-api-reference.md)

[常數 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)

[範例應用程式 &#40;SQLSRV 驅動程式&#41;](../../connect/php/example-application-sqlsrv-driver.md)  
  
