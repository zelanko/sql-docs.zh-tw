---
description: Windows 上適用於 SQL Server 的 Microsoft ODBC 驅動程式
title: Windows 版 Microsoft ODBC Driver for SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b10cfc22-6a2c-4707-a456-0dcec317982b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 38d897f60b5e3ed9278214c8dae8525c72668e20
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727355"
---
# <a name="microsoft-odbc-driver-for-sql-server-on-windows"></a>Windows 上適用於 SQL Server 的 Microsoft ODBC 驅動程式
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Microsoft ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 是獨立的 ODBC 驅動程式，可提供應用程式開發介面 (API) 以實作 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的標準 ODBC 介面。

Microsoft ODBC Driver for SQL Server 可用來建立新的應用程式。 您也可以升級目前使用較舊 ODBC 驅動程式的舊版應用程式。 ODBC Driver for SQL Server 支援連線到 Azure SQL Database、Azure SQL 資料倉儲和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  

## <a name="summary"></a>摘要

| 版本       | 支援的功能      |
| ------------- |---------------| 
| Microsoft ODBC Driver 17 for SQL Server | <ul><li>BCP API 的 Always Encrypted 支援</li><li>新連接字串屬性 UseFMTONLY 會導致驅動程式在需要暫存資料表的特殊案例中使用舊版中繼資料</li>
| Microsoft ODBC Driver 13.1 for SQL Server     | <ul><li>Always Encrypted</li><li>Azure AD 驗證</li><li>AlwaysOn 可用性群組 (AG)</li></ul>   | 
| Microsoft ODBC Driver 13 for SQL Server      | <ul><li>國際化網域名稱 (IDN)</li></ul> |
| Microsoft ODBC Driver 11 for SQL Server | <ul><li>可感知驅動程式的連接共用</li><li>連接恢復功能</li><li>非同步執行 (輪詢方法)</li></ul> |    

## <a name="documentation"></a>文件  
Microsoft ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的文件包括：  
  
-   [ODBC to SQL Server on Windows 版本資訊](../../../connect/odbc/windows/release-notes-odbc-sql-server-windows.md)  
-   [Windows 上 Microsoft ODBC Driver for SQL Server 的功能](../../../connect/odbc/windows/features-of-the-microsoft-odbc-driver-for-sql-server-on-windows.md)  
-   [系統需求、安裝和驅動程式檔案](../../../connect/odbc/windows/system-requirements-installation-and-driver-files.md)  
-   [ODBC Driver for SQL Server 中可感知驅動程式的連接共用](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md)  
-   [非同步執行 &#40;通知方法&#41; 範例](../../../connect/odbc/windows/asynchronous-execution-notification-method-sample.md)  
-   [Windows ODBC 驅動程式中的連接恢復功能](../../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)  
-   [搭配使用 Always Encrypted 與 JDBC 驅動程式](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)
-   [搭配 ODBC 驅動程式使用 Azure Active Directory](../../../connect/odbc/using-azure-active-directory.md) 
-   [使用透明網路 IP 解析](../../../connect/odbc/using-transparent-network-ip-resolution.md)   

## <a name="community"></a>社群  
- [SQL Server 驅動程式部落格](https://techcommunity.microsoft.com/t5/sql-server/bg-p/SQLServer/label-name/SQLServerDrivers)  
- [SQL Server 資料存取論壇](https://social.technet.microsoft.com/Forums/en/sqldataaccess/threads)  
  
## <a name="see-also"></a>另請參閱  
- [使用 SQL Server Native Client 建置應用程式](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)   
- [SQL Server Native Client 常見問題集](/previous-versions/aa937707(v=msdn.10))   
- [ODBC 程式設計人員參考](../../../odbc/reference/odbc-programmer-s-reference.md)   
- [SQL Server Native Client (ODBC)](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)