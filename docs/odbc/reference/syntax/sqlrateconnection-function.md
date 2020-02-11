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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68053646"
---
# <a name="sqlrateconnection-function"></a>SQLRateConnection 函式
**標準**  
 引進的版本： ODBC 3.81 標準合規性： ODBC  
  
 **摘要**  
 **SQLRateConnection**會判斷驅動程式是否可以重複使用連接集區中的現有連接。  
  
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
 源代表新應用程式連接要求的 token 控制碼。  
  
 *hCandidateConnection*  
 源連接集區中的現有連接。 連接必須處於已開啟狀態。  
  
 *fRequiredTransactionEnlistment*  
 源若為 TRUE，針對新的連線要求重複使用現有連接的*hCandidateConnection* （*hRequest*），需要額外的登記。  
  
 *transId*  
 源如果*fRequiredTransactionEnlistment*為 TRUE， *transId*代表要求將登錄的 DTC 交易。 如果*fRequiredTransactionEnlistment*為 FALSE，則會忽略*transId* 。  
  
 *pRating*  
 輸出*hCandidateConnection*的*hRequest*重複使用評等。 此評等會介於0到100（含）之間。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 驅動程式管理員不會處理從此函式傳回的診斷資訊。  
  
## <a name="remarks"></a>備註  
 **SQLRateConnection**會產生介於0與100（含）之間的分數，指出現有連接與要求的相符程度。  
  
|Score|意義（當傳回 SQL_SUCCESS 時）|  
|-----------|-----------------------------------------------|  
|0|*hCandidateConnection*不得重複用於*hRequest*。|  
|介於1到98（含）之間的任何值|分數越高， *hCandidateConnection*與*hRequest*的比對越接近。|  
|99|無意義的屬性中只有不相符的。  驅動程式管理員應該停止分級迴圈。|  
|100|完全相符。  驅動程式管理員應該停止分級迴圈。|  
|任何大於100的其他值|*hCandidateConnection*會標示為「無作用」，而且即使在未來的連接要求中也不會重複使用。|  
  
 如果傳回碼不是 SQL_SUCCESS （包括 SQL_SUCCESS_WITH_INFO）或評等大於100，驅動程式管理員會將連線標示為「無效」。 該無作用的連線將不會重複使用（即使在未來的連接要求中），而且最終會在 CPTimeout 通過之後超時。 驅動程式管理員會繼續從集區尋找另一個連線，以進行分級。  
  
 如果驅動程式管理員重複使用其分數嚴格小於100（包括99）的連線，驅動程式管理員將會呼叫 SQLSetConnectAttr （SQL_ATTR_DBC_INFO_TOKEN），將連線重設回應用程式所要求的狀態。 驅動程式不應在此函式呼叫中重設連接。  
  
 如果*fRequiredTransactionEnlistment*為 TRUE，重複使用*hCandidateConnection*需要額外的登記（*transId* ！ = null）或 unenlistment （*transId* = = null）。 這表示重複使用連接的成本，以及如果驅動程式要在連接時，是否應登錄/取消登錄該連線。 如果*fRequireTransactionEnlistment*為 FALSE，則驅動程式應該忽略*transId*的值。  
  
 驅動程式管理員保證*hRequest*和*HCANDIDATECONNECTION*的父系 HENV 控制碼相同。 驅動程式管理員保證與*hRequest*和*hCandidateConnection*相關聯的集區識別碼相同。  
  
 應用程式不應直接呼叫此函式。 支援可感知驅動程式之連接共用的 ODBC 驅動程式必須實作用此函式。  
  
 包含適用于 ODBC 驅動程式開發的 sqlspi。  
  
## <a name="see-also"></a>另請參閱  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [驅動程式感知的連接共用](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [在 ODBC 驅動程式中開發連線集區覺察](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
