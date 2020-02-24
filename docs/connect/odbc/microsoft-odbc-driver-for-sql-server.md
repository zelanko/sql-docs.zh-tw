---
title: Microsoft ODBC Driver for SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 02/05/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 9f2ae91b-06af-4c9a-9d24-062df7bc4662
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 442a6ad69681a257355d5743d10cb4f933008b8a
ms.sourcegitcommit: 1b0906979db5a276b222f86ea6fdbe638e6c9719
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2020
ms.locfileid: "76971324"
---
# <a name="microsoft-odbc-driver-for-sql-server"></a>Microsoft ODBC Driver for SQL Server

[!INCLUDE[ODBC_Current_Version](../../includes/odbc-latest-release.md)]

[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

ODBC 是以 C 及 C++ 撰寫之 SQL Server 應用程式的主要原生資料存取 API。 大部分的資料來源都有 ODBC 驅動程式。 可以使用 ODBC 的其他語言包括 COBOL、Perl、PHP 和 Python。 ODBC 廣泛使用於資料整合案例。

ODBC 驅動程式隨附 [**sqlcmd**](../../tools/sqlcmd-utility.md) 及 [**bcp**](../../tools/bcp-utility.md) 等多種工具。 **sqlcmd** 公用程式可讓您執行 Transact-SQL 陳述式、系統程序及 SQL 指令碼。 **bcp** 公用程式可在 Microsoft SQL Server 執行個體與使用者所選格式的資料檔案之間大量複製資料。 您可以使用 **bcp** 將大量的新資料列匯入 SQL Server 資料表中，或將資料從資料表匯出到資料檔案中。  

## <a name="code-example-in-c"></a>C++ 程式碼範例

下列 C++ 範例示範如何使用 ODBC API 來連線及存取資料庫：

- [使用 ODBC 的 C++ 程式碼範例](../../odbc/reference/sample-odbc-program.md)

## <a name="download"></a>下載

- ![Download-DownArrow-Circled](../../ssdt/media/download.png)[下載 ODBC 驅動程式](download-odbc-driver-for-sql-server.md)

## <a name="documentation"></a>文件

### <a name="features"></a>特性

- [自訂金鑰儲存區提供者](../../connect/odbc/custom-keystore-providers.md)
- [資料分類](../../connect/odbc/data-classification.md)
- [DSN 和連接字串關鍵字和屬性](dsn-connection-string-attribute.md)
- [SQL Server Native Client](../../relational-databases/native-client/features/sql-server-native-client-features.md) (可用的功能也適用於 ODBC Driver for SQL Server，不含 OLEDB)
- [使用 Always Encrypted](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)
- [使用 Azure Active Directory](../../connect/odbc/using-azure-active-directory.md)
- [使用透明網路 IP 解析](../../connect/odbc/using-transparent-network-ip-resolution.md)
- [使用 XA 交易](../../connect/odbc/use-xa-with-dtc.md)

### <a name="linux-and-macos"></a>Linux 與 macOS

- [安裝驅動程式](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)
- [連線到 SQL Server](../../connect/odbc/linux-mac/connection-string-keywords-and-data-source-names-dsns.md)
- [使用 **bcp** 進行連線](../../connect/odbc/linux-mac/connecting-with-bcp.md)
- [使用 **sqlcmd** 進行連線](../../connect/odbc/linux-mac/connecting-with-sqlcmd.md)
- [資料存取追蹤](../../connect/odbc/linux-mac/data-access-tracing-with-the-odbc-driver-on-linux.md)
- [常見問題集](../../connect/odbc/linux-mac/frequently-asked-questions-faq-for-odbc-linux.md)
- [安裝驅動程式管理員](../../connect/odbc/linux-mac/installing-the-driver-manager.md)
- [已知問題](../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)
- [程式設計指導方針](../../connect/odbc/linux-mac/programming-guidelines.md)
- [版本資訊](../../connect/odbc/linux-mac/release-notes-odbc-sql-server-linux-mac.md)
- [高可用性與災害復原的支援](../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)
- [使用整合式驗證 (Kerberos)](../../connect/odbc/linux-mac/using-integrated-authentication.md)

### <a name="windows"></a>Windows

- [非同步執行 (通知方法) 範例](../../connect/odbc/windows/asynchronous-execution-notification-method-sample.md)
- [Windows ODBC 驅動程式中的連接恢復功能](../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)
- [可感知驅動程式的連接共用](../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md)
- [功能與行為變更](../../connect/odbc/windows/features-of-the-microsoft-odbc-driver-for-sql-server-on-windows.md)
- [ODBC to SQL Server on Windows 版本資訊](windows/release-notes-odbc-sql-server-windows.md)
- [系統需求、安裝和驅動程式檔案](../../connect/odbc/windows/system-requirements-installation-and-driver-files.md)



## <a name="community"></a>社群  
- [Microsoft ODBC Driver For SQL Server 小組部落格](https://blogs.msdn.com/sqlnativeclient/default.aspx)  
- [SQL Server 資料存取論壇](https://social.technet.microsoft.com/Forums/en/sqldataaccess/threads)  
