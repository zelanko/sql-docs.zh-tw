---
description: SQLRateConnection 函式
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cc6b217e8d9e06c4ab011d15cfe016dfefc91d76
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487119"
---
# <a name="sqlrateconnection-function"></a>SQLRateConnection 函式
**一致性**  
 引進的版本： ODBC 3.81 標準合規性： ODBC  
  
 **總結**  
 **SQLRateConnection** 會判斷驅動程式是否可以重複使用連接集區中的現有連接。  
  
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
 輸出權杖控制碼，代表新的應用程式連接要求。  
  
 *hCandidateConnection*  
 輸出連接集區中的現有連接。 連接必須處於開啟狀態。  
  
 *fRequiredTransactionEnlistment*  
 輸出若為 TRUE，則為新的連接要求重複使用現有的連線 *hCandidateConnection* (*hRequest*) 需要額外的登記。  
  
 *transId*  
 輸出如果 *fRequiredTransactionEnlistment* 為 TRUE，則 *transId* 代表要求將登記的 DTC 交易。 如果 *fRequiredTransactionEnlistment* 為 FALSE，則會忽略 *transId* 。  
  
 *pRating*  
 出 *hCandidateConnection*對 *hRequest*的重複使用評等。 此評等會介於0和 100 (內含) 之間。  
  
## <a name="returns"></a>傳回  
 SQL_SUCCESS、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 驅動程式管理員不會處理從此函式傳回的診斷資訊。  
  
## <a name="remarks"></a>備註  
 **SQLRateConnection** 會產生介於0與100之間的分數 (內含) 指出現有的連線與要求的符合程度。  
  
|分數|表示傳回 SQL_SUCCESS 時 () |  
|-----------|-----------------------------------------------|  
|0|*hCandidateConnection* 不得針對 *hRequest*重複使用。|  
|介於1和 98 (包含) 之間的任何值|分數愈高， *hCandidateConnection* 與 *hRequest*的比對越接近。|  
|99|無意義的屬性中只會有不符的情況。  驅動程式管理員應該停止評等迴圈。|  
|100|完全相符。  驅動程式管理員應該停止評等迴圈。|  
|大於100的其他任何值|*hCandidateConnection* 會標示為無作用，即使在未來的連接要求中也不會重複使用。|  
  
 如果傳回碼不是 SQL_SUCCESS (包含 SQL_SUCCESS_WITH_INFO) 或評等大於100，驅動程式管理員會將連接標示為「無作用」。 即使在未來的連線要求中，也不會重複使用該不正確連線 () ，而且最終會在 CPTimeout 通過之後超時。 驅動程式管理員會繼續尋找集區中的另一個連線以進行評分。  
  
 如果驅動程式管理員重複使用的連線，其分數完全小於 100 (包括 99) ，驅動程式管理員會呼叫 SQLSetConnectAttr (SQL_ATTR_DBC_INFO_TOKEN) ，以將連接重設回應用程式所要求的狀態。 此驅動程式不應在此函式呼叫中重設連接。  
  
 如果 *fRequiredTransactionEnlistment* 為 TRUE，重複使用 *hCandidateConnection* 需要額外的登記 (*transId* ！ = null) 或 unenlistment (*transId* = = null) 。 這表示重複使用連接的成本，以及如果驅動程式將會重複使用連線，是否應登錄/取消登錄連接。 如果 *fRequireTransactionEnlistment* 為 FALSE，驅動程式應該忽略 *transId*的值。  
  
 驅動程式管理員保證 *hRequest* 和 *HCANDIDATECONNECTION* 的父 HENV 控制碼相同。 驅動程式管理員可保證與 *hRequest* 和 *hCandidateConnection* 相關聯的集區識別碼都相同。  
  
 應用程式不應該直接呼叫此函數。 支援驅動程式感知連接共用的 ODBC 驅動程式必須執行此函數。  
  
 包含用於 ODBC 驅動程式開發的 sqlspi .h。  
  
## <a name="see-also"></a>另請參閱  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [驅動程式感知連接共用](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [在 ODBC 驅動程式中開發連接集區覺察](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
