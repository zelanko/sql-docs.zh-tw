---
description: SQLSetConnectAttrForDbcInfo 函式
title: SQLSetConnectAttrForDbcInfo 函式 |Microsoft Docs
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
ms.openlocfilehash: 7380ba8682deb7424c363b28d42ecf3980755daf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499558"
---
# <a name="sqlsetconnectattrfordbcinfo-function"></a>SQLSetConnectAttrForDbcInfo 函式
**一致性**  
 引進的版本： ODBC 3.81 標準合規性： ODBC  
  
 **總結**  
 **SQLSetConnectAttrForDbcInfo** 與 **SQLSetConnectAttr**相同，但它會在連接資訊權杖上設定屬性，而不是在連接控制碼上設定屬性。  
  
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
 輸出權杖控制碼。  
  
 *Attribute*  
 輸出要設定的屬性。 有效的屬性清單是驅動程式特定的，與 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)相同。  
  
 *ValuePtr*  
 輸出要與 *屬性*相關聯之值的指標。 根據 *屬性*的值， *ValuePtr* 會是32位不帶正負號的整數值，或指向以 null 結束的字元字串。 請注意，如果 *屬性* 引數是驅動程式特定的值，則 *ValuePtr* 中的值可能是帶正負號的整數。  
  
 *StringLength*  
 輸出如果 *attribute* 是 ODBC 定義的屬性，而且 *ValuePtr* 指向字元字串或二進位緩衝區，此引數應該是 **ValuePtr*的長度。 若為字元字串資料，這個引數應該包含字串中的位元組數目。  
  
 如果 *attribute* 是 ODBC 定義的屬性，而且 *ValuePtr* 是整數，則會忽略 *StringLength* 。  
  
 如果 *屬性* 是驅動程式定義的屬性，則應用程式會藉由設定 *StringLength* 引數來指出驅動程式管理員的屬性性質。 *StringLength* 可以有下列值：  
  
-   如果 *ValuePtr* 是字元字串的指標，則 *StringLength* 是字串或 SQL_NTS 的長度。  
  
-   如果 *ValuePtr* 是二進位緩衝區的指標，則應用程式會將 SQL_LEN_BINARY_ATTR (*長度*) 宏的結果放在 *StringLength*中。 這會在 *StringLength*中放置負數值。  
  
-   如果 *ValuePtr* 是字元字串或二進位字串以外的值指標，則 *StringLength* 應該具有 SQL_IS_POINTER 的值。  
  
-   如果 *ValuePtr* 包含固定長度的值，則 *StringLength* 會視情況 SQL_IS_INTEGER 或 SQL_IS_UINTEGER。  
  
## <a name="returns"></a>傳回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 與[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)相同，不同之處在于驅動程式管理員會使用**HandleType**的 SQL_HANDLE_DBC_INFO_TOKEN 和*hDbcInfoToken*的**控制碼**。  
  
## <a name="remarks"></a>備註  
 **SQLSetConnectAttrForDbcInfo** 與 **SQLSetConnectAttr**相同，但它會在連接資訊標記上設定屬性，而不是在連接控制碼上。 例如，如果 **SQLSetConnectAttr** 無法辨識屬性， **SQLSetConnectAttrForDbcInfo** 也應該傳回該屬性的 SQL_ERROR。  
  
 當驅動程式傳回 SQL_ERROR 或 SQL_INVALID_HANDLE 時，驅動程式應該忽略此屬性來計算集區識別碼。 此外，驅動程式管理員會從 *hDbcInfoToken*取得診斷資訊，並將 SQL_SUCCESS_WITH_INFO 傳回至 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 和 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)中的應用程式。 因此，應用程式可以取得無法設定某些屬性之原因的詳細資料。  
  
 應用程式不應該直接呼叫此函數。 支援驅動程式感知連接共用的 ODBC 驅動程式必須執行此函數。  
  
 包含用於 ODBC 驅動程式開發的 sqlspi .h。  
  
## <a name="see-also"></a>另請參閱  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [驅動程式感知連接共用](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [在 ODBC 驅動程式中開發連接集區覺察](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
