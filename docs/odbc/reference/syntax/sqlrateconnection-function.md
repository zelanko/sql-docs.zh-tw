---
title: "SQLRateConnection 函式 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLRateConnection function [ODBC]
ms.assetid: e8da2ffb-d6ef-4ca7-824f-57afd29585d8
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e63a6312a6f4b637d13282e25311204ea3879fd5
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlrateconnection-function"></a>SQLRateConnection 函式
**一致性**  
 版本引進了： ODBC 3.81 標準相容性： ODBC  
  
 **摘要**  
 **SQLRateConnection**判斷驅動程式可以重複使用現有的連接，連接集區中。  
  
## <a name="syntax"></a>語法  
  
```  
SQLRETURN  SQLRateConnection(  
                SQLHDBC_INFO_TOKEN   hRequest,  
                SQLHDBC              hCandidateConnection,  
                BOOL                 fRequiredTransactionEnlistment,  
                TRANSID              transId,  
                DWORD *              pRating );  
```  
  
## <a name="arguments"></a>引數  
 *hRequest*  
 [輸入]語彙基元的控制代碼，代表新的應用程式連線要求。  
  
 *hCandidateConnection*  
 [輸入]連接集區中現有的連接。 連接必須為開啟狀態。  
  
 *fRequiredTransactionEnlistment*  
 [輸入]如果為 TRUE，重複使用現有的連接*hCandidateConnection*的新連線要求 (*hRequest*) 需要額外的編列。  
  
 *transId*  
 [輸入]如果*fRequiredTransactionEnlistment*為 TRUE， *transId*代表會登記要求的 DTC 交易。 如果*fRequiredTransactionEnlistment*為 FALSE， *transId*會被忽略。  
  
 *pRating*  
 [輸出]*hCandidateConnection*的重複使用評等來*hRequest*。 此分級會是 0 和 100 （含） 之間。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 驅動程式管理員不會處理此函式所傳回的診斷資訊。  
  
## <a name="remarks"></a>備註  
 **SQLRateConnection**會產生介於 0 到 100 （含），表示現有的連線與要求的相符程度的分數。  
  
|分數|（當都會傳回 SQL_SUCCESS） 的意義|  
|-----------|-----------------------------------------------|  
|0|*hCandidateConnection*不得重複使用於*hRequest*。|  
|介於 1 到 98 （含） 之間的任何值|分數越高，越接近， *hCandidateConnection*符合*hRequest*。|  
|99|無意義的屬性有只不符。  驅動程式管理員應該先停止分級迴圈。|  
|100|完美的相符項目。  驅動程式管理員應該先停止分級迴圈。|  
|大於 100 的任何其他值|*hCandidateConnection*標示為寄不出，而且將不會重複使用即使是在未來的連線要求。|  
  
 如果傳回的程式碼 （包括 SQL_SUCCESS_WITH_INFO） 的 SQL_SUCCESS 以外的任何或評等大於 100，驅動程式管理員會將標示為寄不出的連接。 無作用連接不能重複使用 （即使在未來的連線要求），將最後會逾時之後 CPTimeout 傳遞。 驅動程式管理員，仍找不到另一個連接從集區，以進行評價。  
  
 如果驅動程式管理員重複使用其分數會嚴格小於 100 （含 99） 的連接，驅動程式管理員會呼叫 SQLSetConnectAttr(SQL_ATTR_DBC_INFO_TOKEN) 重設回應用程式所要求的狀態連線。 驅動程式應該不會重設這個函式呼叫中的連接。  
  
 如果*fRequiredTransactionEnlistment*為 TRUE，重複使用*hCandidateConnection*需要額外的登錄 (*transId* ！ = NULL) 或 unenlistment (*transId* = = NULL)。 這表示重複使用的連接和驅動程式是否應該登錄 / 取消登錄的連接，如果要重複使用連接的成本。 如果*fRequireTransactionEnlistment*為 FALSE，驅動程式應忽略的值*transId*。  
  
 驅動程式管理員可確保 HENV 處理的父系*hRequest*和*hCandidateConnection*都相同。 驅動程式管理員可以保證與都有相關聯的集區識別碼*hRequest*和*hCandidateConnection*都相同。  
  
 應用程式不應該直接呼叫此函式。 支援可感知驅動程式的連接集區的 ODBC 驅動程式必須實作此函式。  
  
 包含 sqlspi.h ODBC 驅動程式開發。  
  
## <a name="see-also"></a>另請參閱  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [可感知驅動程式的連接共用](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [開發中的 ODBC 驅動程式的連接集區感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
