---
title: "Microsoft ODBC Driver for SQL Server on Windows |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b10cfc22-6a2c-4707-a456-0dcec317982b
caps.latest.revision: 37
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: be37bf73c0fe662b15c8ad26210ed243b5ca317c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/27/2017

---
# <a name="microsoft-odbc-driver-for-sql-server-on-windows"></a>Windows 上適用於 SQL Server 的 Microsoft ODBC 驅動程式
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Microsoft ODBC Driver 13.1、 13 和 11 for[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]是獨立的 ODBC 驅動程式提供給 Microsoft 的標準 ODBC 介面的實作應用程式開發介面 (API) [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。

Microsoft ODBC Driver for SQL Server 可以用來建立新的應用程式。 您也可以升級舊版應用程式目前使用較舊 ODBC 驅動程式。 ODBC Driver for SQL Server 支援連接到 Azure SQL Database、 Azure SQL 資料倉儲、 SQL Server 2016、 SQL Server 2014、 SQL Server 2012、 SQL Server 2008 R2、 SQL Server 2008 和 SQL Server 2005。  

## <a name="summary"></a>摘要

| Version       | 支援的功能      |
| ------------- |---------------| 
| Microsoft ODBC Driver 13.1 for SQL Server     | <ul><li>永遠加密</li><li>Azure AD 驗證</li><li>AlwaysOn 可用性群組 (AG)</li></ul>   | 
| Microsoft ODBC Driver 13 for SQL Server      | <ul><li>國際化網域名稱 (IDN)</li></ul> |
| Microsoft ODBC Driver 11 for SQL Server | <ul><li>可感知驅動程式的連接共用</li><li>連接恢復功能</li><li>非同步執行 （輪詢方法）</li></ul> |    

## <a name="documentation"></a>文件集  
Microsoft ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 的文件包括：  
  
-   [版本資訊](../../../connect/odbc/windows/release-notes.md)  
-   [Microsoft ODBC Driver for SQL Server on Windows 的功能](../../../connect/odbc/windows/features-of-the-microsoft-odbc-driver-for-sql-server-on-windows.md)  
-   [系統需求、安裝和驅動程式檔案](../../../connect/odbc/windows/system-requirements-installation-and-driver-files.md)  
-   [ODBC Driver for SQL Server 中可感知驅動程式的連接共用](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md)  
-   [非同步執行 &#40;通知方法&#41; 範例](../../../connect/odbc/windows/asynchronous-execution-notification-method-sample.md)  
-   [Windows ODBC 驅動程式中的連接恢復功能](../../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)  
-   [使用 ODBC 驅動程式搭配使用一律加密](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)
-   [使用 Azure Active Directory 的 ODBC 驅動程式](../../../connect/odbc/using-azure-active-directory.md) 
-   [使用透明網路 IP 解析](../../../connect/odbc/using-transparent-network-ip-resolution.md)   

## <a name="community"></a>社群  
- [Microsoft ODBC Driver For SQL Server 小組部落格](http://blogs.msdn.com/sqlnativeclient/default.aspx)  
- [SQL Server Data Access Forum](http://social.technet.microsoft.com/Forums/en/sqldataaccess/threads)  
  
## <a name="see-also"></a>另請參閱  
- [關於 SQL Server Native Client](https://msdn.microsoft.com/sqlserver/ff658532.aspx)   
- [使用 SQL Server Native Client 建立應用程式](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)   
- [SQL Server Native Client 常見問題集](https://msdn.microsoft.com/sqlserver/aa937707.aspx)   
- [ODBC 程式設計人員參考](../../../odbc/reference/odbc-programmer-s-reference.md)   
- [SQL Server Native Client (ODBC)](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  

