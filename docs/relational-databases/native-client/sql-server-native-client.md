---
title: "SQL Server Native Client |Microsoft 文件"
ms.date: 04/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e4d4fe39-0090-42a7-8405-6378370d11cb
caps.latest.revision: "43"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Active
ms.openlocfilehash: 7474d620d96880396e8fe7dc44e55b4cdcf7f440
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="sql-server-native-client"></a>SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

SNAC、 或 SQL Server Native Client，是已經用於交換使用適用於 SQL Server，請參閱 ODBC 和 OLE DB 驅動程式的詞彙。 

**如需詳細資訊，並下載 SNAC 或 ODBC 驅動程式，請造訪[所說明的 SNAC 生命週期](https://blogs.msdn.microsoft.com/sqlreleaseservices/snac-lifecycle-explained/)。**

如需有關 ODBC Driver for SQL Server，請參閱[Microsoft ODBC Driver for SQL Server on Windows](https://msdn.microsoft.com/library/jj730314(v=sql.110).aspx)。  此外，請參閱[介紹新的 Microsoft ODBC Driver for SQL Server](https://blogs.msdn.microsoft.com/sqlnativeclient/2013/01/23/introducing-the-new-microsoft-odbc-drivers-for-sql-server/)，和[ODBC Driver 13.1 for SQL Server 發行](https://blogs.technet.microsoft.com/dataplatforminsider/2016/08/03/odbc-driver-13-1-for-sql-server-released/)。  
  
 有關[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端功能隨附[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，最後使用的 SQL Server native Client 版本： 
  
-   [SQL Server Native Client 支援 LocalDB](../../relational-databases/native-client/features/sql-server-native-client-support-for-localdb.md)  
  
-   [中繼資料探索](../../relational-databases/native-client/features/metadata-discovery.md)  
  
-   [SQL Server Native Client 11.0 中的 UTF-16 支援](../../relational-databases/native-client/features/utf-16-support-in-sql-server-native-client-11-0.md)  
  
-   [高可用性、 災害復原的 SQL Server Native Client 支援](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  
  
-   [存取擴充事件記錄檔中的診斷資訊](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)  
  
中的 ODBC[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端支援新增至 Windows 7 SDK 中的標準 ODBC 的三個功能：  
  
-   連接相關作業的非同步執行。 如需詳細資訊，請參閱[非同步執行](http://go.microsoft.com/fwlink/?LinkID=191493)。  
  
-   C 資料類型擴充性。 如需詳細資訊，請參閱[ODBC 中的 C 資料類型](http://go.microsoft.com/fwlink/?LinkID=191495)。  
  
     若要支援這項功能[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端，可以傳回 SQLGetDescField **SQL_C_SS_TIME2** (如**時間**類型) 或**SQL_C_SS_TIMESTAMPOFFSET** （適用於**datetimeoffset**) 而不是**SQL_C_BINARY**，如果您的應用程式使用 ODBC 3.8 的話。 如需詳細資訊，請參閱[ODBC 日期和時間增強功能的資料類型支援](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md)。  
  
-   呼叫**SQLGetData**使用小型緩衝區多次，以便擷取大型參數值。 如需詳細資訊，請參閱[使用 SQLGetData 擷取輸出參數](http://go.microsoft.com/fwlink/?LinkID=191494)。  
  
 下列主題描述的是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client 行為變更。  
  
-   當呼叫**icommandwithparameters:: Setparameterinfo**，傳遞給的值*pwszName*參數必須是有效的識別項。 如需詳細資訊，請參閱[ICommandWithParameters](../../relational-databases/native-client-ole-db-interfaces/icommandwithparameters.md)。  
  
-   **SQLDescribeParam**會一致地傳回 ODBC 規格合格值。 如需詳細資訊，請參閱[SQLDescribeParam](../../relational-databases/native-client-odbc-api/sqldescribeparam.md)。  
  
-   [ODBC 驅動程式在處理字元轉換上的行為變更](../../relational-databases/native-client/features/odbc-driver-behavior-change-when-handling-character-conversions.md)  
  
## <a name="see-also"></a>另請參閱  
[安裝 SQL Server Native Client](../../relational-databases/native-client/applications/installing-sql-server-native-client.md)  
 [SQL Server Native Client 功能](../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
