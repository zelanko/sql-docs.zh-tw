---
title: 在處理字元轉換 ODBC 驅動程式行為變更 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 682a232a-bf89-4849-88a1-95b2fbac1467
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b7f9562f8594e29c33832c595b9296eaf4f2019b
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52540185"
---
# <a name="odbc-driver-behavior-change-when-handling-character-conversions"></a>ODBC 驅動程式在處理字元轉換上的行為變更
  [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client ODBC 驅動程式 (SQLNCLI11.dll) 改變了其的 SQL_WCHAR * (處理和 SQL_CHAR\* （NARCHAR 轉換。 當使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2012 Native Client ODBC 驅動程式時，ODBC 函數如 SQLGetData、SQLBindCol、SQLBindParameter 等傳回的長度/指標參數將會是 (-4) SQL_NO_TOTAL。 舊版的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式以往傳回長度值，而這可能不正確。  
  
## <a name="sqlgetdata-behavior"></a>SQLGetData 行為  
 許多 Windows 函數都可讓您指定緩衝區大小為 0，且傳回的長度會是所傳回資料的大小。 以下的寫法對 Windows 程式設計人員而言應已司空見慣：  
  
```  
int iSize = 0;  
BYTE * pBuffer = NULL;  
GetMyFavoriteAPI(pBuffer, &iSize);   // Returns needed size in iSize  
pBuffer = new BYTE[iSize];   // Allocate buffer   
GetMyFavoriteAPI(pBuffer, &iSize);   // Retrieve actual data  
```  
  
 不過， **SQLGetData**不應在此案例中。 請勿使用這種寫法：  
  
```  
// bad  
int iSize = 0;  
WCHAR * pBuffer = NULL;  
SQLGetData(hstmt, SQL_W_CHAR, ...., (SQLPOINTER*)0x1, 0, &iSize);   // Get storage size needed  
pBuffer = new WCHAR[(iSize/sizeof(WCHAR)) + 1];   // Allocate buffer  
SQLGetData(hstmt, SQL_W_CHAR, ...., (SQLPOINTER*)pBuffer, iSize, &iSize);   // Retrieve data  
```  
  
 **SQLGetData**只可以呼叫以擷取實際的資料區塊。 使用**SQLGetData**若要取得的資料大小不是不受支援。  
  
 以下說明當您使用不正確的寫法時，驅動程式變更所造成的影響。 此應用程式將查詢 `varchar` 資料行並以 Unicode (SQL_UNICODE/SQL_WCHAR) 的形式進行繫結：  
  
 查詢：  `select convert(varchar(36), '123')`  
  
```  
SQLGetData(hstmt, SQL_WCHAR, ....., (SQLPOINTER*) 0x1, 0 , &iSize);   // Attempting to determine storage size needed  
```  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式版本|長度或指標結果|描述|  
|-----------------------------------------------------------------|---------------------------------|-----------------|  
|[!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] Native Client 或更早版本|6|驅動程式誤認為只要長度 * 2 即可將 CHAR 轉換成 WCHAR。|  
|[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client (11.0.2100.60 版) 或更新版本|-4 (SQL_NO_TOTAL)|驅動程式不再認為從 CHAR 轉換成 WCHAR 或 WCHAR 到 CHAR 的 （乘） \*2 或 （除法） / 2 的動作。<br /><br /> 呼叫**SQLGetData**不會再傳回預期轉換後的長度。 驅動程式將偵測出這是 CHAR 與 WCHAR 之間的相互轉換，並且傳回 (-4) SQL_NO_TOTAL 而不至於會有 *2 或 /2 的錯誤行為。|  
  
 使用**SQLGetData**來擷取資料區塊。 (虛擬程式碼如下所示)  
  
```  
while( (SQL_SUCCESS or SQL_SUCCESS_WITH_INFO) == SQLFetch(...) ) {  
   SQLNumCols(...iTotalCols...)  
   for(int iCol = 1; iCol < iTotalCols; iCol++) {  
      WCHAR* pBufOrig, pBuffer = new WCHAR[100];  
      SQLGetData(.... iCol ... pBuffer, 100, &iSize);   // Get original chunk  
      while(NOT ALL DATA RETREIVED (SQL_NO_TOTAL, ...) ) {  
         pBuffer += 50;   // Advance buffer for data retrieved  
         // May need to realloc the buffer when you reach current size  
         SQLGetData(.... iCol ... pBuffer, 100, &iSize);   // Get next chunk  
      }  
   }  
}  
```  
  
## <a name="sqlbindcol-behavior"></a>SQLBindCol 行為  
 查詢：  `select convert(varchar(36), '1234567890')`  
  
```  
SQLBindCol(... SQL_W_CHAR, ...)   // Only bound a buffer of WCHAR[4] - Expecting String Data Right Truncation behavior  
```  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式版本|長度或指標結果|描述|  
|-----------------------------------------------------------------|---------------------------------|-----------------|  
|[!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] Native Client 或更早版本|20|-   **SQLFetch**回報資料右側截斷。<br />長度是傳回的資料，儲存的內容長度 (假設 * WCHAR 轉換可能會不正確的字符的 2 個字元)。<br />-儲存在緩衝區中的資料是 123 \ 0。 緩衝區一定是以 NULL 結尾。|  
|[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client (11.0.2100.60 版) 或更新版本|-4 (SQL_NO_TOTAL)|-   **SQLFetch**回報資料右側截斷。<br />由於資料的其餘部分並未轉換，長度會指出-4 (SQL_NO_TOTAL)。<br />-儲存在緩衝區中的資料是 123 \ 0。 - 緩衝區一定是以 NULL 結尾。|  
  
## <a name="sqlbindparameter-output-parameter-behavior"></a>SQLBindParameter (OUTPUT 參數行為)  
 查詢：  `create procedure spTest @p1 varchar(max) OUTPUT`  
  
 `select @p1 = replicate('B', 1234)`  
  
```  
SQLBindParameter(... SQL_W_CHAR, ...)   // Only bind up to first 64 characters  
```  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式版本|長度或指標結果|描述|  
|-----------------------------------------------------------------|---------------------------------|-----------------|  
|[!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] Native Client 或更早版本|2468|-   **SQLFetch**傳回沒有可用的詳細資料。<br />-   **SQLMoreResults**傳回沒有可用的詳細資料。<br />長度會指出傳回的伺服器，不會儲存在緩衝區資料的大小。<br />-原始緩衝區內包含 63 個位元組和 NULL 結束字元。 緩衝區一定是以 NULL 結尾。|  
|[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client (11.0.2100.60 版) 或更新版本|-4 (SQL_NO_TOTAL)|-   **SQLFetch**傳回沒有可用的詳細資料。<br />-   **SQLMoreResults**傳回沒有可用的詳細資料。<br />由於資料的其餘部分並未轉換，長度會指出 (-4) SQL_NO_TOTAL。<br />-原始緩衝區內包含 63 個位元組和 NULL 結束字元。 緩衝區一定是以 NULL 結尾。|  
  
## <a name="performing-char-and-wchar-conversions"></a>執行 CHAR 和 WCHAR 轉換  
 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client ODBC 驅動程式提供了幾種方法來執行 CHAR 和 WCHAR 轉換。 邏輯是類似於操作 blob （varchar （max)、 nvarchar （max），...）：  
  
-   資料會儲存或使用繫結時，截斷至指定的緩衝區**SQLBindCol**或是**SQLBindParameter**。  
  
-   如果您不會繫結，您可以使用擷取區塊中的資料**SQLGetData**並**SQLParamData**。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client 功能](sql-server-native-client-features.md)  
  
  
