---
title: "從 SQL Server 2005 Native Client 將應用程式更新 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|applications
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client, updating applications
ms.assetid: 1e1e570c-7f14-4e16-beab-c328e3fbdaa8
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7a0765a262b2775f81b35969a638ff6f3583357e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="updating-an-application-from-sql-server-2005-native-client"></a>從 SQL Server 2005 Native Client 更新應用程式
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  本主題討論自 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 起，[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Native Client 中的重大變更。  
  
 當您從 Microsoft Data Access Components (MDAC) 升級為 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 時，可能也會看見一些行為差異。 如需詳細資訊，請參閱[更新至 SQL Server Native Client 應用程式從 MDAC](../../../relational-databases/native-client/applications/updating-an-application-to-sql-server-native-client-from-mdac.md)。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 9.0 隨附[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 10.0 隨附[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]。  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.5 隨附於 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)]。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 隨附於 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 和 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]。  
  
|自從 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以來，SQL Server Native Client 中已經變更的行為|Description|  
|------------------------------------------------------------------------------------|-----------------|  
|OLE DB 只會填補至定義的小數位數。|轉換的轉換後的資料傳送到伺服器， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (從[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) 之資料的最大長度只限尾端零填補**datetime**值。 SQL Server Native Client 9.0 則會填滿至 9 位數。|  
|如 ICommandWithParameter::SetParameterInfo 驗證 DBTYPE_DBTIMESTAMP。|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client (從[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) 實作的 OLE DB 需求*bScale*中 ICommandWithParameter::SetParameterInfo 針對 DBTYPE_DBTIMESTAMP 設定為小數的秒數有效位數。|  
|**Sp_columns**預存程序現在會傳回**"NO"**而不是**"NO"** IS_NULLABLE 資料行。|從開始[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 10.0 ([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)])， **sp_columns**預存程序現在會傳回**"NO"**而不是**"NO"** IS_NULLABLE 資料行.|  
|SQLSetDescRec、 SQLBindParameter 等和 SQLBindCol 現在執行一致性檢查。|之前[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 10.0 中，設定 sql_desc_data_ptr 並不會造成任何描述項類型的一致性檢查 SQLSetDescRec、 SQLBindParameter 等或 SQLBindCol 中。|  
|SQLCopyDesc 現在會描述項一致性檢查。|之前[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 10.0，SQLCopyDesc 一致性檢查時未在特定記錄上設定 SQL_DESC_DATA_PTR 欄位。|  
|SQLGetDescRec 不再不描述項一致性檢查。|之前[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 10.0 中，設定 SQL_DESC_DATA_PTR 欄位時，SQLGetDescRec 執行描述項一致性檢查。 這不是 ODBC 規格所需，而且在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 ([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) 和更新版本中，將不再執行這項一致性檢查。|  
|當日期超出範圍時傳回不同錯誤。|**Datetime**類型，將所傳回不同的錯誤數目[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]原生用戶端 (從[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) 的範圍外的日期與舊版中傳回。<br /><br /> 具體來說， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 會針對所有超出範圍的年份值在字串轉換為傳回 22007 **datetime**，和[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 10.0 版的開頭 ([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) 傳回 22008 時日期是所支援的範圍內**datetime2**所支援的範圍外**datetime**或**smalldatetime**。|  
|**datetime**值會截斷小數秒數和 round 如果不在四捨五入會改變日期。|之前[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 10.0 的用戶端行為**datetime**傳送到伺服器的值是要四捨五入到最接近的 1/300 秒。 從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 開始，這個情況會造成小數秒被截斷 (如果四捨五入會改變日期的話)。|  
|可能會截斷秒為單位的**datetime**值。|如果您繫結至類型識別碼為 DBTYPE_DBTIMESTAMP (OLE DB) 或 SQL_TIMESTAMP (ODBC) 且小數位數為 0 的 datetime 資料行，則使用 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client (或更新版本) 建置並且連接至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2005 伺服器的應用程式，將會截斷傳送至伺服器的資料中時間部分的秒和小數秒。<br /><br /> 例如：<br /><br /> 輸入資料：1994-08-21 21:21:36.000<br /><br /> 插入的資料：1994-08-21 21:21:00.000|  
|從 DBTYPE_DBTIME 轉換成 DBTYPE_DATE 的 OLE DB 資料轉換作業不會再造成日期變更。|在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 之前，如果 DBTYPE_DATE 的時間部分在午夜的半秒鐘之內，OLE DB 轉換程式碼會造成日期變更。 從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 開始，日期將不會變更 (小數秒會被截斷，而且不會四捨五入)。|  
|IBCPSession::BCColFmt 轉換變更。|從開始[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]匯出 Native Client 10.0 中，當您使用 IBCPSession::BCOColFmt 將 SQLDATETIME 或 SQLDATETIME 轉換成字串類型，小數的值。 例如，將 SQLDATETIME 類型轉換成 SQLNVARCHARMAX 類型時，便會傳回舊版的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client。<br /><br /> 1989-02-01 00:00:00. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 和更新版本會傳回 1989-02-01 00:00:00.0000000。|  
|傳送的資料大小必須符合 SQL_LEN_DATA_AT_EXEC 中指定的長度。|當使用 SQL_LEN_DATA_AT_EXEC 時，資料的大小必須符合您使用 SQL_LEN_DATA_AT_EXEC 所指定的長度。 您可以使用 SQL_DATA_AT_EXEC，但是使用 SQL_LEN_DATA_AT_EXEC 可能會有效能上的好處。|  
|使用 BCP API 的自訂應用程式現在可以看到警告。|如果資料長度大於所有類型之欄位所指定的長度，BCP API 將會產生一則警告訊息。 之前這個警告只針對字元類型來提供，但是將不會針對所有類型發出。|  
|將空字串插入**sql_variant**繫結為日期/時間類型會產生錯誤。|在[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 9.0 中，將空字串插入**sql_variant**繫結為日期/時間類型不會產生錯誤。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 (和更新版本) 在這種情況下會正確地產生錯誤。|  
|更嚴格的 SQL_C_TYPE _TIMESTAMP 和 DBTYPE_DBTIMESTAMP 參數驗證。|之前[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]Native Client， **datetime**值四捨五入，以符合的標尺**datetime**和**smalldatetime**依資料行[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client (和更新版本) 套用的驗證規則，要比 ODBC 核心規格內針對小數秒所定義的規則更嚴格。 如果一定要截斷尾端位數，才能使用用戶端繫結所指定或默許的小數位數來將參數值轉換成 SQL 類型，便會傳回錯誤。|  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可能會在觸發程序執行時傳回不同的結果。|中導入變更[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]可能會導致應用程式有不同的結果造成觸發程序時要執行的陳述式所傳回**NOCOUNT OFF**作用中。 在此狀況下，您的應用程式可能會產生錯誤。 若要解決這個錯誤，將**NOCOUNT ON**觸發程序呼叫中 SQLMoreResults 前進至下一個結果。|  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client 程式設計](../../../relational-databases/native-client/sql-server-native-client-programming.md)  
  
  
