---
title: SQLSetConnecttfordbcinfo 功能 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectAttrForDbcInfo function [ODBC]
ms.assetid: a28fadb9-b998-472a-b252-709507e92005
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9f43a0fc6cd02fe566579a543667f9a4c4c1a108
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301885"
---
# <a name="sqlsetconnectattrfordbcinfo-function"></a>SQLSetConnectAttrForDbcInfo 函式
**一致性**  
 版本介紹: ODBC 3.81 標準合規性: ODBC  
  
 **摘要**  
 **SQLSetConnectTrForDbcInfo**與**SQLSetConnectAttr**相同,但它在連接資訊權杖上而不是在連接句柄上設定屬性。  
  
## <a name="syntax"></a>語法  
  
```cpp
  
SQLRETURN  SQLSetConnectAttrForDbcInfo(  
                SQLHDBC_INFO_TOKEN    hDbcInfoToken,  
                SQLINTEGER            Attribute,  
                SQLPOINTER            ValuePtr,  
                SQLINTEGER            StringLength );  
```  
  
## <a name="arguments"></a>引數  
 *hDbcInfoToken*  
 [輸入]令牌句柄。  
  
 *屬性*  
 [輸入]要設置的屬性。 有效屬性的清單特定於驅動程式,與[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)相同。  
  
 *ValuePtr*  
 [輸入]指向要與*屬性*關聯的值的指標。 根據*屬性*的值 *,ValuePtr*將是一個 32 位元未符號整數值,或將指向 null 端接的字串。 請注意,如果*屬性*參數是特定於驅動程式的值 *,ValuePtr*中的值可能是已簽名的整數。  
  
 *字串長度*  
 [輸入]如果*屬性*是 ODBC 定義的屬性 *,ValuePtr*指向字串或二進位緩衝區,則此參數應為 **ValuePtr*的長度。 對於字串資料,此參數應包含字串中的位元組數。  
  
 如果*屬性*是 ODBC 定義的屬性 *,ValuePtr*是整數,則忽略*字串長度*。  
  
 如果*屬性*是驅動程式定義的屬性,則應用程式通過設置*StringLength*參數指示該屬性對驅動程式管理員的性質。 *字串長度*可以具有以下值:  
  
-   如果*ValuePtr*是指向字串的指標,則*StringLength*是字串的長度或SQL_NTS。  
  
-   如果*ValuePtr*是指向二進位緩衝區的指標,則應用程式將SQL_LEN_BINARY_ATTR(*長度*)宏的結果放在*StringLength 中*。 這將在*字串長度*中放置負值。  
  
-   如果*ValuePtr*是指向字串或二進位元字串以外的值的指標,則*StringLength*應具有該值SQL_IS_POINTER。  
  
-   如果*ValuePtr*包含固定長度值,則*StringLength*會根據需要SQL_IS_INTEGER或SQL_IS_UINTEGER。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 與[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)相同,只不過驅動程式管理員會使用SQL_HANDLE_DBC_INFO_TOKEN的**句柄類型**與*hDbcInfoToken*的**句柄**。  
  
## <a name="remarks"></a>備註  
 **SQLSetConnectTrForDbcInfo**與**SQLSetConnectAttr**相同,但它在連接資訊令牌上設置屬性,而不是在連接句柄上設置屬性。 例如,如果**SQLSetConnectAttr**無法識別屬性,**則 SQLSetConnect AttrForDbcInfo**也應返回該屬性SQL_ERROR。  
  
 每當驅動程式返回SQL_ERROR或SQL_INVALID_HANDLE時,驅動程式應忽略此屬性以計算池 ID。 此外,驅動程式管理器將從*hDbcInfoToken*獲取診斷資訊,並將SQL_SUCCESS_WITH_INFO返回到[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)和[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)中的應用程式。 因此,應用程式可以檢索有關無法設置某些屬性的原因的詳細資訊。  
  
 應用程式不應直接調用此功能。 支援驅動程式感知連接池的ODBC驅動程式必須實現此功能。  
  
 包括用於 ODBC 驅動程式開發的 sqlspi.h。  
  
## <a name="see-also"></a>另請參閱  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [驅動程式感知連接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [在 ODBC 驅動程式中開發連接集區覺察](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
