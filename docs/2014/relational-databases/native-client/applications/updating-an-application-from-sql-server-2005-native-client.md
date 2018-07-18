---
title: 從 SQL Server 2005 Native Client 將應用程式更新 |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client  - "database-engine" - "docset-sql-devref"
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client, updating applications
ms.assetid: 1e1e570c-7f14-4e16-beab-c328e3fbdaa8
caps.latest.revision: 42
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 956e7aa2befcd53c2d18a2d1530fae7fdad0a0f2
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37413328"
---
# <a name="updating-an-application-from-sql-server-2005-native-client"></a>從 SQL Server 2005 Native Client 更新應用程式
  本主題討論自 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 起，[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Native Client 中的重大變更。  
  
 當您從 Microsoft Data Access Components (MDAC) 升級為 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 時，可能也會看見一些行為差異。 如需詳細資訊，請參閱 <<c0> [ 更新至 SQL Server Native Client 應用程式從 MDAC](updating-an-application-to-sql-server-native-client-from-mdac.md)。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 隨附[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 隨附[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]。  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.5 隨附於 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)]。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 隨附於 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 和 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]。  
  
|自從 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以來，SQL Server Native Client 中已經變更的行為|描述|  
|------------------------------------------------------------------------------------|-----------------|  
|OLE DB 只會填補至定義的小數位數。|如果轉換作業會將轉換的資料傳送給伺服器，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (從 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 開始) 最多只會在資料中用尾端零填滿至 `datetime` 值的最大長度。 SQL Server Native Client 9.0 則會填滿至 9 位數。|  
|驗證 ICommandWithParameter::SetParameterInfo 的 DBTYPE_DBTIMESTAMP。|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (從[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) 實作的 OLE DB 需求*bScale*可針對 DBTYPE_DBTIMESTAMP 設定為小數秒精確度的 ICommandWithParameter::SetParameterInfo 中。|  
|`sp_columns`預存程序現在會傳回 **[否]** 而非 **"NO"** IS_NULLABLE 資料行。|從開始[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 10.0 ([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)])，`sp_columns`預存程序現在會傳回 **「 否 」** 而非 **"NO"** 針對 IS_NULLABLE 資料行。|  
|SQLSetDescRec、 SQLBindParameter 等和 SQLBindCol 現在會執行一致性檢查。|之前[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 10.0 中，設定 sql_desc_data_ptr 並不會造成任何描述項類型的一致性檢查 SQLSetDescRec、 SQLBindParameter 等或 SQLBindCol 中。|  
|SQLCopyDesc 現在會執行描述項一致性檢查。|之前[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 10.0，SQLCopyDesc 沒有一致性檢查的特定記錄上設定 SQL_DESC_DATA_PTR 欄位時。|  
|SQLGetDescRec 不再會描述項一致性檢查。|之前[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 10.0 中，設定 SQL_DESC_DATA_PTR 欄位時，SQLGetDescRec 執行描述項一致性檢查。 這不是 ODBC 規格所需，而且在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 ([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) 和更新版本中，將不再執行這項一致性檢查。|  
|當日期超出範圍時傳回不同錯誤。|如果是 `datetime` 類型，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (從 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 開始) 將會針對超出範圍的日期傳回與舊版不同的錯誤號碼。<br /><br /> 具體而言，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 會針對轉換為 `datetime` 之字串內所有超出範圍的年份值傳回 22007，而從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 版 ([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) 開始，則會在日期位於 `datetime2` 支援的範圍內但是超出 `datetime` 或 `smalldatetime` 的支援範圍時，傳回 22008。|  
|`datetime` 值會截斷小數秒且不會四捨五入 (如果四捨五入會改變日期的話)。|在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 之前，傳送給伺服器之 `datetime` 值的用戶端行為是要四捨五入到最接近的 1/300 秒。 從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 開始，這個情況會造成小數秒被截斷 (如果四捨五入會改變日期的話)。|  
|可能會截斷 `datetime` 值的秒數。|如果您繫結至類型識別碼為 DBTYPE_DBTIMESTAMP (OLE DB) 或 SQL_TIMESTAMP (ODBC) 且小數位數為 0 的 datetime 資料行，則使用 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client (或更新版本) 建置並且連接至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2005 伺服器的應用程式，將會截斷傳送至伺服器的資料中時間部分的秒和小數秒。<br /><br /> 例如：<br /><br /> 輸入資料：1994-08-21 21:21:36.000<br /><br /> 插入的資料：1994-08-21 21:21:00.000|  
|從 DBTYPE_DBTIME 轉換成 DBTYPE_DATE 的 OLE DB 資料轉換作業不會再造成日期變更。|在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 之前，如果 DBTYPE_DATE 的時間部分在午夜的半秒鐘之內，OLE DB 轉換程式碼會造成日期變更。 從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 開始，日期將不會變更 (小數秒會被截斷，而且不會四捨五入)。|  
|IBCPSession::BCColFmt 轉換變更。|從開始[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]匯出 Native Client 10.0 中，當您使用 IBCPSession::BCOColFmt 將 SQLDATETIME 或 SQLDATETIME 轉換成字串類型，小數的值。 例如，將 SQLDATETIME 類型轉換成 SQLNVARCHARMAX 類型時，便會傳回舊版的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client。<br /><br /> 1989-02-01 00:00:00. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 和更新版本會傳回 1989-02-01 00:00:00.0000000。|  
|傳送的資料大小必須符合 SQL_LEN_DATA_AT_EXEC 中指定的長度。|當使用 SQL_LEN_DATA_AT_EXEC 時，資料的大小必須符合您使用 SQL_LEN_DATA_AT_EXEC 所指定的長度。 您可以使用 SQL_DATA_AT_EXEC，但是使用 SQL_LEN_DATA_AT_EXEC 可能會有效能上的好處。|  
|使用 BCP API 的自訂應用程式現在可以看到警告。|如果資料長度大於所有類型之欄位所指定的長度，BCP API 將會產生一則警告訊息。 之前這個警告只針對字元類型來提供，但是將不會針對所有類型發出。|  
|將空字串插入繫結為日期/時間類型的 `sql_variant` 中會產生錯誤。|在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 中，將空字串插入繫結為日期/時間類型的 `sql_variant` 中並不會產生錯誤。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 (和更新版本) 在這種情況下會正確地產生錯誤。|  
|更嚴格的 SQL_C_TYPE _TIMESTAMP 和 DBTYPE_DBTIMESTAMP 參數驗證。|之前[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]原生用戶端`datetime`值四捨五入，以符合的小數位數`datetime`並`smalldatetime`資料行[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client (和更新版本) 套用的驗證規則，要比 ODBC 核心規格內針對小數秒所定義的規則更嚴格。 如果一定要截斷尾端位數，才能使用用戶端繫結所指定或默許的小數位數來將參數值轉換成 SQL 類型，便會傳回錯誤。|  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可能會在觸發程序執行時傳回不同的結果。|[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 中導入的變更可能會使得應用程式從陳述式中傳回不同的結果，該陳述式會在 `NOCOUNT OFF` 有效時造成觸發程序的執行。 在此狀況下，您的應用程式可能會產生錯誤。 若要解決這個錯誤，將`NOCOUNT ON`中觸發程序或呼叫 SQLMoreResults 前進到下一個結果。|  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client 程式設計](../sql-server-native-client-programming.md)  
  
  
