---
title: 關於
description: 瞭解 SQL Server Native Client 的功能（SNAC）。 SQL Server Native Client 是指 SQL Server 的 ODBC 和 OLE DB 驅動程式。
ms.date: 04/14/2017
ms.prod: sql
ms.reviewer: ''
ms.custom: ''
ms.technology: native-client
ms.topic: conceptual
ms.assetid: e4d4fe39-0090-42a7-8405-6378370d11cb
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 829b6dccd12edaa707a2aad2d0861c75e99c408e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85787588"
---
# <a name="sql-server-native-client"></a>SQL Server Native Client
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

SNAC （或 SQL Server Native Client）是一種詞彙，可交換用來參考 ODBC 和 OLE DB 驅動程式以進行 SQL Server。

> [!IMPORTANT] 
> SQL Server Native Client （SQLNCLI）仍會被取代，不建議將它用於新的開發工作。 請改為使用新的 [Microsoft OLE DB Driver for SQL Server](../../connect/oledb/oledb-driver-for-sql-server.md) (MSOLEDBSQL)，其會進行更新且具備最新的伺服器功能。

> [!NOTE]
> 如需詳細資訊及下載 SNAC 或 ODBC 驅動程式，請參閱[SNAC 生命週期說明的 blog 文章](https://blogs.msdn.microsoft.com/sqlreleaseservices/snac-lifecycle-explained/)。
> 如需 ODBC Driver for SQL Server 的詳細資訊，請參閱[Microsoft ODBC Driver for SQL Server](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md)。  

 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]隨附的 Native client 功能的資訊 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ，SQL Server native client 的最後一個可用版本：

-   [SQL Server Native Client 對 LocalDB 的支援](../../relational-databases/native-client/features/sql-server-native-client-support-for-localdb.md)  

-   [中繼資料探索](../../relational-databases/native-client/features/metadata-discovery.md)  

-   [SQL Server Native Client 11.0 中的 UTF-16 支援](../../relational-databases/native-client/features/utf-16-support-in-sql-server-native-client-11-0.md)  

-   [高可用性/災害復原的 SQL Server Native Client 支援](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  

-   [存取擴充事件記錄檔中的診斷資訊](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)  

Native Client 中的 ODBC [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援在 Windows 7 SDK 中新增至標準 odbc 的三項功能：  

-   連接相關作業的非同步執行。 如需詳細資訊，請參閱[非同步執行](https://go.microsoft.com/fwlink/?LinkID=191493)。  

-   C 資料類型擴充性。 如需詳細資訊，請參閱[ODBC 中的 C 資料類型](https://go.microsoft.com/fwlink/?LinkID=191495)。  

     若要在 Native Client 中支援這項功能 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，如果您的應用程式使用 ODBC 3.8，SQLGetDescField 可以傳回**SQL_C_SS_TIME2** （適用于**時間**類型）或**SQL_C_SS_TIMESTAMPOFFSET** （適用于**datetimeoffset**），而不是**SQL_C_BINARY**。 如需詳細資訊，請參閱[資料類型對 ODBC 日期和時間改善的支援](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md)。  

-   多次呼叫具有小型緩衝區的**SQLGetData** ，以取出大型參數值。 如需詳細資訊，請參閱[使用 SQLGetData 抓取輸出參數](https://go.microsoft.com/fwlink/?LinkID=191494)。  

 下列主題描述的是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client 行為變更。  

-   呼叫**ICommandWithParameters：： SetParameterInfo**時，傳遞至*pwszName*參數的值必須是有效的識別碼。 如需詳細資訊，請參閱[ICommandWithParameters](../../relational-databases/native-client-ole-db-interfaces/icommandwithparameters.md)。  

-   **SQLDescribeParam**會一致地傳回符合 ODBC 規格的值。 如需詳細資訊，請參閱[SQLDescribeParam](../../relational-databases/native-client-odbc-api/sqldescribeparam.md)。  

-   [ODBC 驅動程式在處理字元轉換上的行為變更](../../relational-databases/native-client/features/odbc-driver-behavior-change-when-handling-character-conversions.md)  

## <a name="see-also"></a>另請參閱  
[安裝 SQL Server Native Client](../../relational-databases/native-client/applications/installing-sql-server-native-client.md)  
 [SQL Server Native Client 功能](../../relational-databases/native-client/features/sql-server-native-client-features.md)  
