---
title: SQL Server Native Client 的新功能&#39;|Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: e4d4fe39-0090-42a7-8405-6378370d11cb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d2a01b9d9d13bf5e9135d287553beb8b87c2dcd5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62638849"
---
# <a name="what39s-new-in-sql-server-native-client"></a>SQL Server Native Client 的新功能&#39;
  
  [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 會安裝 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client。 沒有 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Native Client。  
  
 未來 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 的 ODBC 驅動程式不會再更新。 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 隨附安裝 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Native Client ODBC 驅動程式的後續版本 (在 Windows 上稱為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC Driver 11 for [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)])。 如需有關在 Windows [!INCLUDE[msCoName](../../includes/msconame-md.md)]上的 odbc driver [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 11 for 的詳細資訊，請參閱[Microsoft odbc Driver 11 for SQL Server-windows](https://www.microsoft.com/download/details.aspx?id=36434)。  
  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 中的 OLE DB 提供者上次在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client 中更新。 開發人員若要使用 OLE DB 提供者連接到最新版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，必須使用 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client 隨附的 OLE DB 提供者。  
  
 下列主題將描述 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的全新 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client 功能。  
  
-   [SQL Server Native Client 對 LocalDB 的支援](features/sql-server-native-client-support-for-localdb.md)  
  
-   [中繼資料探索](features/metadata-discovery.md)  
  
-   [SQL Server Native Client 11.0 中的 UTF-16 支援](features/utf-16-support-in-sql-server-native-client-11-0.md)  
  
-   [高可用性/災害復原的 SQL Server Native Client 支援](features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  
  
-   [存取擴充事件記錄檔中的診斷資訊](features/accessing-diagnostic-information-in-the-extended-events-log.md)  
  
 此外，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 中的 ODBC 現在支援三項已加入至 Windows 7 SDK 中之標準 ODBC 的功能：  
  
-   連接相關作業的非同步執行。 如需詳細資訊，請參閱[非同步執行](https://go.microsoft.com/fwlink/?LinkID=191493)。  
  
-   C 資料類型擴充性。 如需詳細資訊，請參閱[ODBC 中的 C 資料類型](https://go.microsoft.com/fwlink/?LinkID=191495)。  
  
     若要在 Native Client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中支援這項功能， `SQL_C_SS_TIME2`如果您`time`的`SQL_C_BINARY`應用程式`SQL_C_SS_TIMESTAMPOFFSET`使用 ODBC `datetimeoffset`3.8，SQLGetDescField 可以傳回（適用于類型）或（適用于）而不是。 如需詳細資訊，請參閱[資料類型對 ODBC 日期和時間改善的支援](features/date-and-time-improvements.md)。  
  
-   使用小型緩衝區多次呼叫 `SQLGetData`，以便擷取大型參數值。 如需詳細資訊，請參閱[使用 SQLGetData 抓取輸出參數](https://go.microsoft.com/fwlink/?LinkID=191494)。  
  
 下列主題描述的是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client 行為變更。  
  
-   呼叫`ICommandWithParameters::SetParameterInfo`時，傳遞至*pwszName*參數的值必須是有效的識別碼。 如需詳細資訊，請參閱[ICommandWithParameters](../native-client-ole-db-interfaces/icommandwithparameters.md)。  
  
-   
  `SQLDescribeParam` 現在會一致地傳回符合 ODBC 規格的值。 如需詳細資訊，請參閱[SQLDescribeParam](../native-client-odbc-api/sqldescribeparam.md)。  
  
-   [ODBC 驅動程式在處理字元轉換上的行為變更](features/odbc-driver-behavior-change-when-handling-character-conversions.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client 功能](features/sql-server-native-client-features.md)  
  
  
