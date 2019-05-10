---
title: SQL Server Native Client |Microsoft Docs
ms.date: 04/14/2017
ms.prod: sql
ms.reviewer: ''
ms.custom: ''
ms.technology: native-client
ms.topic: conceptual
ms.assetid: e4d4fe39-0090-42a7-8405-6378370d11cb
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b39b71f65dfe9c41c3e2ea7282729691e78a5986
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/09/2019
ms.locfileid: "65484518"
---
# <a name="sql-server-native-client"></a>SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

SNAC 或 SQL Server Native Client，指的是，已用交換來參考適用於 SQL Server 的 ODBC 和 OLE DB 驅動程式。

> [!IMPORTANT] 
> SQL Server Native Client (SQLNCLI) 會保持已被取代，並不建議用於新的開發工作。 相反地，使用 新[Microsoft OLE DB Driver for SQL Server](../../connect/oledb/oledb-driver-for-sql-server.md) (MSOLEDBSQL) 這會更新為最新的伺服器功能。

> [!NOTE]
> 如需詳細資訊及下載的 SNAC 或 ODBC 驅動程式，請參閱[SNAC 生命週期所述的部落格文章](https://blogs.msdn.microsoft.com/sqlreleaseservices/snac-lifecycle-explained/)。
> 如需有關 ODBC Driver for SQL Server，請參閱[Microsoft ODBC Driver for SQL Server](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md)。  

 有關[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client 功能隨附[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，SQL Server native Client 的最後一個可用版本：

-   [SQL Server Native Client 支援 LocalDB](../../relational-databases/native-client/features/sql-server-native-client-support-for-localdb.md)  

-   [中繼資料探索](../../relational-databases/native-client/features/metadata-discovery.md)  

-   [SQL Server Native Client 11.0 中的 UTF-16 支援](../../relational-databases/native-client/features/utf-16-support-in-sql-server-native-client-11-0.md)  

-   [高可用性/災害復原的 SQL Server Native Client 支援](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  

-   [存取擴充事件記錄檔中的診斷資訊](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)  

中的 ODBC[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端支援新增至 Windows 7 SDK 中的標準 ODBC 的三個功能：  

-   連接相關作業的非同步執行。 如需詳細資訊，請參閱 <<c0> [ 非同步執行](https://go.microsoft.com/fwlink/?LinkID=191493)。  

-   C 資料類型擴充性。 如需詳細資訊，請參閱 < [ODBC 中的 C 資料類型](https://go.microsoft.com/fwlink/?LinkID=191495)。  

     若要支援這項功能[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端，可以傳回 SQLGetDescField **SQL_C_SS_TIME2** (如**時間**類型) 或**SQL_C_SS_TIMESTAMPOFFSET** （適用於**datetimeoffset**) 而非**SQL_C_BINARY**，如果您的應用程式使用 ODBC 3.8 的話。 如需詳細資訊，請參閱 <<c0> [ 資料類型對 ODBC 日期和時間改善支援](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md)。  

-   呼叫**SQLGetData**使用小型緩衝區多次，以便擷取大型參數值。 如需詳細資訊，請參閱 <<c0> [ 使用 SQLGetData 擷取輸出參數](https://go.microsoft.com/fwlink/?LinkID=191494)。  

 下列主題描述的是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client 行為變更。  

-   當呼叫**icommandwithparameters:: Setparameterinfo**，值傳遞給*pwszName*參數必須是有效的識別項。 如需詳細資訊，請參閱 < [ICommandWithParameters](../../relational-databases/native-client-ole-db-interfaces/icommandwithparameters.md)。  

-   **SQLDescribeParam**會一致地傳回 ODBC 規格相符的值。 如需詳細資訊，請參閱 < [SQLDescribeParam](../../relational-databases/native-client-odbc-api/sqldescribeparam.md)。  

-   [ODBC 驅動程式在處理字元轉換上的行為變更](../../relational-databases/native-client/features/odbc-driver-behavior-change-when-handling-character-conversions.md)  

## <a name="see-also"></a>另請參閱  
[安裝 SQL Server Native Client](../../relational-databases/native-client/applications/installing-sql-server-native-client.md)  
 [SQL Server Native Client 功能](../../relational-databases/native-client/features/sql-server-native-client-features.md)  
