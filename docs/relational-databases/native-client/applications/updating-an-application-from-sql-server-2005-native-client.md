---
title: 從 SQL 2005 更新
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client, updating applications
ms.assetid: 1e1e570c-7f14-4e16-beab-c328e3fbdaa8
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3287f5faf6d748a433a425c1ecf505bbe551d3b2
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388292"
---
# <a name="updating-an-application-from-sql-server-2005-native-client"></a>從 SQL Server 2005 Native Client 更新應用程式
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  本主題討論自 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 起，[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Native Client 中的重大變更。  
  
 當您從 Microsoft Data Access Components (MDAC) 升級為 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 時，可能也會看見一些行為差異。 有關詳細資訊,請參閱從[MDAC 將應用程式更新到 SQL 伺服器本機客戶端](../../../relational-databases/native-client/applications/updating-an-application-to-sql-server-native-client-from-mdac.md)。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 隨附於 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 隨附於 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]。  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.5 隨附於 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)]。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 隨附於 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 和 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]。  
  
|自從 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以來，SQL Server Native Client 中已經變更的行為|描述|  
|------------------------------------------------------------------------------------|-----------------|  
|OLE DB 只會填補至定義的小數位數。|對於將轉換後的資料傳送到伺服器的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]轉換, 本機[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]客戶端(以開頭)的焊盤僅追蹤數據中的零,直到**日期時間**值的最大長度。 SQL Server Native Client 9.0 則會填滿至 9 位數。|  
|驗證 ICommandWithParameter::SetParameterInfo 的 DBTYPE_DBTIMESTAMP。|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本機用戶端(以[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]開頭)在ICommand與參數中實現*bScale*的OLE DB要求::將參數資訊設置為DBTYPE_DBTIMESTAMP的分數秒精度。|  
|**sp_columns** 預存程序現在會針對 IS_NULLABLE 資料行傳回 **"NO"**，而非 **"NO "**。|從[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本機用戶端 10.0[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] **()開始,sp_columns**儲存過程現在返回 **「NO」** 而不是「**否」 IS_NULLABLE**列。|  
|SQLSetDescRec、SQLBind參數和 SQLBindCol 現在執行一致性檢查。|在[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本機用戶端 10.0 之前,設定SQL_DESC_DATA_PTR不會導致 SQLSetDescRec、SQLBind 參數或 SQLBindCol 中任何描述符類型的一致性檢查。|  
|SQLCopyDesc 現在執行描述符一致性檢查。|在[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本機用戶端 10.0 之前,SQLCopyDesc 未在特定記錄上設置SQL_DESC_DATA_PTR欄位時執行一致性檢查。|  
|SQLGetDescRec 不再執行描述符一致性檢查。|在[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本機用戶端 10.0 之前,SQLGetDescRec 在設置SQL_DESC_DATA_PTR欄位時執行描述符一致性檢查。 這不是 ODBC 規格所需，而且在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 ([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) 和更新版本中，將不再執行這項一致性檢查。|  
|當日期超出範圍時傳回不同錯誤。|對於**日期時間**類型,[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本機用戶端([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]以開頭)將返回與早期版本中返回的不同錯誤編號。<br /><br /> 具體來說,[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本機用戶端 9.0 返回 22007 字串轉換到**日期時間**的所有超出[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]範圍的年份值, 和本機[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]用戶端從版本 10.0 ( ) 開始返回 22008 當日期在**datetime2**支援的範圍,但超出**日期時間**或**小日期時間**支援的範圍。|  
|**datetime** 值會截斷小數秒且不會四捨五入 (如果四捨五入會改變日期的話)。|在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 之前，傳送給伺服器之 **datetime** 值的用戶端行為是要四捨五入到最接近的 1/300 秒。 從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 開始，這個情況會造成小數秒被截斷 (如果四捨五入會改變日期的話)。|  
|可能會截斷 **datetime** 值的秒數。|如果您繫結至類型識別碼為 DBTYPE_DBTIMESTAMP (OLE DB) 或 SQL_TIMESTAMP (ODBC) 且小數位數為 0 的 datetime 資料行，則使用 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client (或更新版本) 建置並且連接至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2005 伺服器的應用程式，將會截斷傳送至伺服器的資料中時間部分的秒和小數秒。<br /><br /> 例如：<br /><br /> 輸入資料：1994-08-21 21:21:36.000<br /><br /> 插入的資料：1994-08-21 21:21:00.000|  
|從 DBTYPE_DBTIME 轉換成 DBTYPE_DATE 的 OLE DB 資料轉換作業不會再造成日期變更。|在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 之前，如果 DBTYPE_DATE 的時間部分在午夜的半秒鐘之內，OLE DB 轉換程式碼會造成日期變更。 從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 開始，日期將不會變更 (小數秒會被截斷，而且不會四捨五入)。|  
|IBCPSession::BCColFmt 轉換變更。|從[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本機用戶端 10.0 開始,當您使用 IBCPSession::BCOColFmt 將 SQLDATETIME 或 SQLDATETIME 轉換為字串類型時,將匯出小數值。 例如，將 SQLDATETIME 類型轉換成 SQLNVARCHARMAX 類型時，便會傳回舊版的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client。<br /><br /> 1989-02-01 00:00:00。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 和更新版本會傳回 1989-02-01 00:00:00.0000000。|  
|傳送的資料大小必須符合 SQL_LEN_DATA_AT_EXEC 中指定的長度。|當使用 SQL_LEN_DATA_AT_EXEC 時，資料的大小必須符合您使用 SQL_LEN_DATA_AT_EXEC 所指定的長度。 您可以使用 SQL_DATA_AT_EXEC，但是使用 SQL_LEN_DATA_AT_EXEC 可能會有效能上的好處。|  
|使用 BCP API 的自訂應用程式現在可以看到警告。|如果資料長度大於所有類型之欄位所指定的長度，BCP API 將會產生一則警告訊息。 之前這個警告只針對字元類型來提供，但是將不會針對所有類型發出。|  
|將空字串插入繫結為日期/時間類型的 **sql_variant** 中會產生錯誤。|在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 中，將空字串插入繫結為日期/時間類型的 **sql_variant** 中並不會產生錯誤。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 (和更新版本) 在這種情況下會正確地產生錯誤。|  
|更嚴格的 SQL_C_TYPE _TIMESTAMP 和 DBTYPE_DBTIMESTAMP 參數驗證。|在[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]本機客戶端之前,**日期時間**值四捨五入,以適合**日期時間和****小日期時間**列[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的縮放 。 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client (和更新版本) 套用的驗證規則，要比 ODBC 核心規格內針對小數秒所定義的規則更嚴格。 如果一定要截斷尾端位數，才能使用用戶端繫結所指定或默許的小數位數來將參數值轉換成 SQL 類型，便會傳回錯誤。|  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可能會在觸發程序執行時傳回不同的結果。|[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 中導入的變更可能會使得應用程式從陳述式中傳回不同的結果，該陳述式會在 **NOCOUNT OFF** 有效時造成觸發程序的執行。 在此狀況下，您的應用程式可能會產生錯誤。 要解決此錯誤,請在觸發器中設置**NOCOUNT ON**或調用 SQLMore 結果以推進到下一個結果。|  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client 程式設計](../../../relational-databases/native-client/sql-server-native-client-programming.md)  
  
  
