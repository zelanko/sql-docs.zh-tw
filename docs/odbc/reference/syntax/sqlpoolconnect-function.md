---
title: SQLPoolConnect 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLPoolConnect function [ODBC]
ms.assetid: 41322737-890d-4a81-aed2-06cc3d546962
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0c390dacb5072c5d516e95b4fe6b789bfffbbd2d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68005807"
---
# <a name="sqlpoolconnect-function"></a>SQLPoolConnect 函式
**合規性**  
 導入的版本：ODBC 3.8 標準合規性：ODBC  
  
 **摘要**  
 **SQLPoolConnect**用來建立新的連接，如果集區中的沒有連線可以重複使用。  
  
## <a name="syntax"></a>語法  
  
```cpp
  
SQLRETURN  SQLPoolConnect(  
                SQLHDBC              hDbc,  
                SQLHDBC_INFO_TOKEN   hDbcInfoToken,  
                WCHAR *              wszOutConnectString,  
                SQLSMALLINT          cchConnectStringBuffer,  
                SQLSMALLINT *        cchConnectStringLen );  
```  
  
## <a name="arguments"></a>引數  
 *hDbc*  
 [輸入]連接控制代碼。  
  
 *hDbcInfoToken*  
 [輸入]新的應用程式連線要求權杖控制代碼。  
  
 *wszOutConnectString*  
 [輸出]已完成的連接字串之緩衝區的指標。 目標資料來源的連接成功，這個緩衝區會包含完整的連接字串。 應用程式應配置這個緩衝區至少 1,024 個字元。  
  
 如果*wszOutConnectString*為 NULL，就*cchConnectStringLen*仍會傳回 （不含字元資料的 null 終止字元） 的字元總數可用來傳回中所指向的緩衝區*wszOutConnectString*。  
  
 *cchConnectStringBuffer*  
 [輸入]長度 **wszOutConnectString*緩衝區，以字元為單位。  
  
 *cchConnectStringLen*  
 [輸出]在其中傳回 （不包括 null 結束字元） 的字元總數緩衝區的指標來傳回在可用\* *wszOutConnectString*。 可用來傳回字元的數目是否大於或等於*cchConnectStringBuffer*，則完成中的連接字串\* *wszOutConnectString*會被截斷成*cchConnectStringBuffer*減去 null 結束字元的長度。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO，SQL_ERROR，或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 類似於[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)任何輸入驗證錯誤時，不同之處在於會使用驅動程式管理員**HandleType** SQL_HANDLE_DBC_INFO_TOKEN 的並**處理**的*hDbcInfoToken*。  
  
## <a name="remarks"></a>備註  
 驅動程式管理員可確保 HENV 處理的父系*hDbc*並*hDbcInfoToken*都相同。  
  
 不同於[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)，沒有任何*DriverCompletion*引數，以提示使用者輸入連接資訊。 共用的案例中，不允許提示的對話方塊。  
  
 應用程式不應該直接呼叫此函式。 支援可感知驅動程式的連接共用的 ODBC 驅動程式必須實作此函式。  
  
 只要驅動程式會傳回 SQL_ERROR 或 SQL_INVALID_HANDLE，驅動程式管理員會傳回錯誤至應用程式 (在[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)或是[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md))。  
  
 只要驅動程式會傳回 SQL_SUCCESS_WITH_INFO，驅動程式管理員會取得的診斷資訊*hDbcInfoToken*，並集中的應用程式會傳回 SQL_SUCCESS_WITH_INFO [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)並[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)。  
  
 當應用程式時，使用[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)， *wszOutConnectString*會是 （最後三個參數將所有設定為 NULL，NULL，0） 的 NULL 緩衝區。 否則，驅動程式必須傳回將傳回給應用程式的輸出連接字串[SQLDriverConnect 函數](../../../odbc/reference/syntax/sqldriverconnect-function.md)呼叫。  
  
 包含 ODBC 驅動程式開發的 sqlspi.h。  
  
## <a name="see-also"></a>另請參閱  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [可感知驅動程式的連接共用](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [在 ODBC 驅動程式中開發連接集區覺察](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
