---
title: SQLSetConnectAttrForDbcInfo 函式 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLSetConnectAttrForDbcInfo function [ODBC]
ms.assetid: a28fadb9-b998-472a-b252-709507e92005
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8ef62393ac00b7d094e6ba47613038fdf7ac2175
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="sqlsetconnectattrfordbcinfo-function"></a>SQLSetConnectAttrForDbcInfo 函式
**一致性**  
 版本引進了： ODBC 3.81 標準相容性： ODBC  
  
 **摘要**  
 **SQLSetConnectAttrForDbcInfo**相同**SQLSetConnectAttr**，但是它上的連線資訊語彙基元而非連接控制代碼上設定的屬性。  
  
## <a name="syntax"></a>語法  
  
```  
SQLRETURN  SQLSetConnectAttrForDbcInfo(  
                SQLHDBC_INFO_TOKEN    hDbcInfoToken,  
                SQLINTEGER            Attribute,  
                SQLPOINTER            ValuePtr,  
                SQLINTEGER            StringLength );  
```  
  
## <a name="arguments"></a>引數  
 *hDbcInfoToken*  
 [輸入]語彙基元的控制代碼。  
  
 *Attribute*  
 [輸入]若要設定的屬性。 有效的屬性清單是特定的驅動程式和一樣[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)。  
  
 *ValuePtr*  
 [輸入]要與相關聯的值指標*屬性*。 值而定*屬性*， *ValuePtr*將會是 32 位元不帶正負號的整數值，或將會指向以 null 結束的字元字串。 請注意，如果*屬性*引數是驅動程式專屬值中的值*ValuePtr*可能是帶正負號的整數。  
  
 *StringLength*  
 [輸入]如果*屬性*是 ODBC 定義的屬性和*ValuePtr*指向字元字串或二進位的緩衝區，這個引數應該是長度 **ValuePtr*。 字元字串資料，這個引數應該包含在字串中的位元組數目。  
  
 如果*屬性*是 ODBC 定義的屬性和*ValuePtr*是整數， *StringLength*會被忽略。  
  
 如果*屬性*是驅動程式定義的屬性，應用程式設定指出屬性給驅動程式管理員性質*StringLength*引數。 *StringLength*可以是下列值：  
  
-   如果*ValuePtr*是字元字串的指標，則*StringLength*是 SQL_NTS 之字串的長度。  
  
-   如果*ValuePtr*是二進位緩衝區的指標，則應用程式會將 SQL_LEN_BINARY_ATTR 結果 (*長度*) 中的巨集*StringLength*。 這樣做會放在負值*StringLength*。  
  
-   如果*ValuePtr*是字元字串或二進位字串以外的值的指標，則*StringLength*應該有 SQL_IS_POINTER 的值。  
  
-   如果*ValuePtr*包含固定長度的值，則*StringLength*是 SQL_IS_INTEGER 或 SQL_IS_UINTEGER，視需要。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 與相同[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)，不同之處在於會使用驅動程式管理員**HandleType**的 SQL_HANDLE_DBC_INFO_TOKEN 和**處理**的*hDbcInfoToken*.  
  
## <a name="remarks"></a>備註  
 **SQLSetConnectAttrForDbcInfo**相同**SQLSetConnectAttr**，但它會設定的屬性上的連線資訊語彙基元，而不是連接控制代碼。 例如，如果**SQLSetConnectAttr**無法辨識的屬性， **SQLSetConnectAttrForDbcInfo**也應該該屬性會傳回 SQL_ERROR。  
  
 驅動程式時驅動程式會傳回 SQL_ERROR 或 SQL_INVALID_HANDLE，應該忽略這個屬性來計算集區識別碼。 此外，驅動程式管理員會取得診斷資訊從*hDbcInfoToken*，並在應用程式傳回 SQL_SUCCESS_WITH_INFO， [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)和[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md). 因此，應用程式可以擷取有關為什麼無法設定某些屬性的詳細資料。  
  
 應用程式不應該直接呼叫此函式。 支援可感知驅動程式的連接集區的 ODBC 驅動程式必須實作此函式。  
  
 包含 sqlspi.h ODBC 驅動程式開發。  
  
## <a name="see-also"></a>請參閱  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [可感知驅動程式的連接共用](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [在 ODBC 驅動程式中開發連接集區覺察](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
