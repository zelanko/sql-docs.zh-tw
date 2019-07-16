---
title: SQLRateConnection 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLRateConnection function [ODBC]
ms.assetid: e8da2ffb-d6ef-4ca7-824f-57afd29585d8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 74d7e2c52167682f0993006db3a1125ca741cf35
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68053646"
---
# <a name="sqlrateconnection-function"></a>SQLRateConnection 函式
**合規性**  
 導入的版本：ODBC 3.81 標準合規性：ODBC  
  
 **摘要**  
 **SQLRateConnection**判斷驅動程式可以重複使用現有的連接，連接集區中。  
  
## <a name="syntax"></a>語法  
  
```cpp
  
SQLRETURN  SQLRateConnection(  
                SQLHDBC_INFO_TOKEN   hRequest,  
                SQLHDBC              hCandidateConnection,  
                BOOL                 fRequiredTransactionEnlistment,  
                TRANSID              transId,  
                DWORD *              pRating );  
```  
  
## <a name="arguments"></a>引數  
 *hRequest*  
 [輸入]語彙基元的控制代碼，表示新的應用程式連線要求。  
  
 *hCandidateConnection*  
 [輸入]連接集區中現有的連接。 連接必須為開啟狀態。  
  
 *fRequiredTransactionEnlistment*  
 [輸入]如果為 TRUE，重複使用現有的連接*hCandidateConnection*的新連線要求 (*hRequest*) 需要額外的登錄。  
  
 *transId*  
 [輸入]如果*fRequiredTransactionEnlistment*為 TRUE 時， *transId*代表要求將會登錄在 DTC 交易。 如果*fRequiredTransactionEnlistment*為 FALSE 時， *transId*將會被忽略。  
  
 *pRating*  
 [輸出]*hCandidateConnection*的重複使用評等來*hRequest*。 此評等會介於 0 到 100 （含） 之間。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 驅動程式管理員不會處理此函式所傳回的診斷資訊。  
  
## <a name="remarks"></a>備註  
 **SQLRateConnection**會產生介於 0 到 100 （含） 表示現有的連線與要求的相符程度的分數。  
  
|分數|（當都會傳回 SQL_SUCCESS） 的意義|  
|-----------|-----------------------------------------------|  
|0|*hCandidateConnection*不會重複用於*hRequest*。|  
|介於 1 和 98 （含） 之間的任何值|分數越高，愈接近所*hCandidateConnection*符合*hRequest*。|  
|99|無意義的屬性有只不相符。  驅動程式管理員應該停止的評等的迴圈。|  
|100|完美的相符項目。  驅動程式管理員應該停止的評等的迴圈。|  
|大於 100 的任何其他值|*hCandidateConnection*標示為無效信件和它將不會重複使用即使在未來的連線要求。|  
  
 如果傳回的程式碼 （包括 SQL_SUCCESS_WITH_INFO） 的 SQL_SUCCESS 以外的任何項目或評等會大於 100，則驅動程式管理員會將標示為無效的連接。 該無作用的連線不能重複使用 （即使在未來的連線要求），以及將最終會逾時 CPTimeout 經過後。 驅動程式管理員會繼續尋找另一個連接從集區的速率。  
  
 如果驅動程式管理員會重複使用其分數會嚴格小於 100 （含 99） 的連接，驅動程式管理員會呼叫 SQLSetConnectAttr(SQL_ATTR_DBC_INFO_TOKEN) 以重設回應用程式所要求的狀態連線。 驅動程式不應該重設此函式呼叫中的連接。  
  
 如果*fRequiredTransactionEnlistment*為 TRUE，重複使用*hCandidateConnection*需要額外的登錄 (*transId* ！ = NULL) 或 unenlistment (*transId* = = NULL)。 這表示重複使用的連接和驅動程式是否應該登錄 / 取消登錄的連線，如果要重複使用連線的成本。 如果*fRequireTransactionEnlistment*為 FALSE 時，驅動程式應忽略的值*transId*。  
  
 驅動程式管理員可確保 HENV 處理的父系*hRequest*並*hCandidateConnection*都相同。 驅動程式管理員可確保與都有相關聯的集區識別碼*hRequest*並*hCandidateConnection*都相同。  
  
 應用程式不應該直接呼叫此函式。 支援可感知驅動程式的連接共用的 ODBC 驅動程式必須實作此函式。  
  
 包含 ODBC 驅動程式開發的 sqlspi.h。  
  
## <a name="see-also"></a>另請參閱  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [可感知驅動程式的連接共用](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [在 ODBC 驅動程式中開發連接集區覺察](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
