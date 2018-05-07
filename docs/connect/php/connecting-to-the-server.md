---
title: 連接到伺服器 |Microsoft 文件
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c251a239-e0bd-4f45-9207-b76651072dd0
caps.latest.revision: 44
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f21d84708f4d1fdb05fe422a5e176187118dae04
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="connecting-to-the-server"></a>連接到伺服器
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本節的主題描述使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 連接到 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的選項和程序。  

[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 可以使用 Windows 驗證或使用 SQL Server 驗證連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 。 根據預設， [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 會嘗試使用 Windows 驗證連接到伺服器。  

## <a name="in-this-section"></a>本節內容  

|主題|Description|  
|---------|---------------|  
|[如何：使用 Windows 驗證進行連接](../../connect/php/how-to-connect-using-windows-authentication.md)|描述如何使用 Windows 驗證建立連接。|  
|[如何：使用 SQL Server 驗證進行連接](../../connect/php/how-to-connect-using-sql-server-authentication.md)|描述如何使用 SQL Server 驗證建立連接。|  
|[如何：使用 Azure Active Directory 驗證進行連線](../../connect/php/azure-active-directory.md)|描述如何設定驗證模式，並使用 Azure Active Directory 身分識別來連接。|  
|[如何：使用指定的連接埠連線](../../connect/php/how-to-connect-on-a-specified-port.md)|描述如何連接到特定連接埠上的伺服器。|  
|[連接共用](../../connect/php/connection-pooling-microsoft-drivers-for-php-for-sql-server.md)|提供有關驅動程式中連接共用的資訊。|  
|[如何：停用 Multiple Active Result Set (MARS)](../../connect/php/how-to-disable-multiple-active-resultsets-mars.md)|描述如何在進行連接時停用 MARS 功能。|  
|[連線選項](../../connect/php/connection-options.md)|列出包含連接屬性的關聯陣列中允許的選項。|  
|[LocalDB 的支援](../../connect/php/php-driver-for-sql-server-support-for-localdb.md)|描述 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 對 LocalDB 功能的支援 (已加入 [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]中)。|  
|[高可用性與災害復原的支援](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)|討論如何設定您的應用程式，以利用加入功能的高可用性、 嚴重損壞修復的[!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]。|  
|[連線到 Microsoft Azure SQL Database](../../connect/php/connecting-to-microsoft-azure-sql-database.md)|討論如何連接到 Azure SQL Database。|  
|[連線恢復功能](../../connect/php/connection-resiliency.md)|討論將重新建立連線中斷連接恢復功能。|  

## <a name="see-also"></a>另請參閱  
[程式程式設計指南 Microsoft Drivers for PHP，適用於 SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)

[範例應用程式 &#40;SQLSRV 驅動程式&#41;](../../connect/php/example-application-sqlsrv-driver.md)  
