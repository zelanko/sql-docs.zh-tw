---
title: 關於
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
ms.openlocfilehash: d175942c9d636221868ca12743e6dac79bb2ddcb
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388711"
---
# <a name="sql-server-native-client"></a>SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

SNAC 或 SQL Server 本機用戶端是一個已互換用於引用 SQL Server 的 ODBC 和 OLE DB 驅動程式的術語。

> [!IMPORTANT] 
> SQL Server 本機用戶端 (SQLNCLI) 仍然被棄用,不建議將其用於新的開發工作。 請改為使用新的 [Microsoft OLE DB Driver for SQL Server](../../connect/oledb/oledb-driver-for-sql-server.md) (MSOLEDBSQL)，其會進行更新且具備最新的伺服器功能。

> [!NOTE]
> 有關詳細資訊並下載 SNAC 或 ODBC 驅動程式,請參閱[SNAC 生命週期解釋部落格文章](https://blogs.msdn.microsoft.com/sqlreleaseservices/snac-lifecycle-explained/)。
> 此 SQL 伺服器的 ODBC 驅動程式的詳細資訊,請參閱[SQL Server 的 Microsoft ODBC 驅動程式](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md)。  

 與[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]釋放[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的本機客戶端功能的資訊,這是 SQL Server 本機客戶端的最後一個可用版本:

-   [SQL Server Native Client 對 LocalDB 的支援](../../relational-databases/native-client/features/sql-server-native-client-support-for-localdb.md)  

-   [中繼資料探索](../../relational-databases/native-client/features/metadata-discovery.md)  

-   [SQL Server Native Client 11.0 中的 UTF-16 支援](../../relational-databases/native-client/features/utf-16-support-in-sql-server-native-client-11-0.md)  

-   [高可用性/災害復原的 SQL Server Native Client 支援](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  

-   [存取擴展事件記錄檔中的診斷資訊](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)  

本機客戶端[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的 ODBC 支援在 Windows 7 SDK 中新增到標準 ODBC 的三個功能:  

-   連接相關作業的非同步執行。 有關詳細資訊,請參閱[非同步執行](https://go.microsoft.com/fwlink/?LinkID=191493)。  

-   C 資料類型擴充性。 關於詳細資訊,請參閱[ODBC 中的 C 資料類型](https://go.microsoft.com/fwlink/?LinkID=191495)。  

     為了在本機客戶端[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中 支援此功能,如果您的應用程式使用 ODBC 3.8,SQLGetDescField 可以返回**SQL_C_SS_TIME2(** 對於**時間**類型)或**SQL_C_SS_TIMESTAMPOFFSET(** 用於**日期時間偏移**),而不是**SQL_C_BINARY。** 關於詳細資訊,請參閱[ODBC 日期與時間改進的資料型態支援](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md)。  

-   多次使用小緩衝區調用**SQLGetData**以檢索大型參數值。 有關詳細資訊,請參閱使用[SQLGetData 檢索輸出參數](https://go.microsoft.com/fwlink/?LinkID=191494)。  

 下列主題描述的是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client 行為變更。  

-   呼叫**ICommand 與參數:::set 參數資訊**時,傳遞給*pwszName*參數的值必須是一個有效的識別碼。 有關詳細資訊,請參閱[ICommand 與參數](../../relational-databases/native-client-ole-db-interfaces/icommandwithparameters.md)。  

-   **SQLDescribeParam**將始終如一地返回符合 ODBC 規範的值。 有關詳細資訊,請參閱[SQL 描述 Param](../../relational-databases/native-client-odbc-api/sqldescribeparam.md)。  

-   [ODBC 驅動程式在處理字元轉換上的行為變更](../../relational-databases/native-client/features/odbc-driver-behavior-change-when-handling-character-conversions.md)  

## <a name="see-also"></a>另請參閱  
[安裝 SQL 伺服器本機用戶端](../../relational-databases/native-client/applications/installing-sql-server-native-client.md)  
 [SQL Server Native Client 功能](../../relational-databases/native-client/features/sql-server-native-client-features.md)  
