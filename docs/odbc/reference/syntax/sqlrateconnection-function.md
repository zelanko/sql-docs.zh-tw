---
title: SQLRate連接功能 |微軟文件
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
ms.openlocfilehash: d29033460a7f89fc4a8b1c371a4d32bdf94a2a05
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288878"
---
# <a name="sqlrateconnection-function"></a>SQLRateConnection 函式
**一致性**  
 版本介紹: ODBC 3.81 標準合規性: ODBC  
  
 **摘要**  
 **SQLRateConnection**確定驅動程式是否可以重用連接池中的現有連接。  
  
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
 *h 要求*  
 [輸入]表示新應用程式連接請求的權杖句柄。  
  
 *h候選人連線*  
 [輸入]連接池中的現有連接。 連接必須處於打開狀態。  
  
 *f 必需交易登記*  
 [輸入]如果為 TRUE,則重新使用現有連接的*h候選連接*以執行新的連接請求 *(hRequest*) 需要額外的登記。  
  
 *轉體*  
 [輸入]如果*f需要交易登記*為 TRUE,transId 表示請求將登記的*transId*DTC 事務。 如果*f"需要交易登記"* 為 FALSE,則將忽略*transId。*  
  
 *放大縮小字型功能 放大縮小字型功能*  
 【輸出]*h 候選連線*的重新使用等級為*hRequest*。 此評級將在 0 和 100 之間(含)。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 驅動程式管理員不會處理從此功能返回的診斷資訊。  
  
## <a name="remarks"></a>備註  
 **SQLRateConnection**生成介於 0 和 100(含)之間的分數,指示現有連接與請求匹配程度。  
  
|Score|含義(返回SQL_SUCCESS時)|  
|-----------|-----------------------------------------------|  
|0|*h候選連線*不得為*hRequest*重複使用。|  
|介於 1 和 98 之間的任何值(含)|分數越高 *,h候選連接*與*hRequest*匹配越近。|  
|99|在微不足道的屬性中,只有不匹配。  驅動程式管理員應停止評級迴圈。|  
|100|完美匹配。  驅動程式管理員應停止評級迴圈。|  
|任何其他大於 100 的值|*h候選連接*標記為已死,即使在將來的連接請求中也不會重複使用。|  
  
 如果返回代碼不是SQL_SUCCESS(包括SQL_SUCCESS_WITH_INFO)或額定值大於 100,則驅動程式管理器將連接標記為已死。 連接不會重複使用(即使在將來的連接請求中),並且最終將在 CPTimeout 通過後超時。 驅動程式管理器將繼續從池中尋找另一個連接以進行速率。  
  
 如果驅動程式管理器重用分數嚴格小於 100(包括 99)的連接,驅動程式管理器將調用 SQLSetConnectAttr(SQL_ATTR_DBC_INFO_TOKEN)將連接重新重置為應用程式請求的狀態。 驅動程式不應在此函數調用中重置連接。  
  
 如果*f"必需交易登記"* 為 TRUE,則重用*h候選連接*需要額外的登記(*轉接*!= NULL)或取消登記(*轉 Id* = NULL)。 這表示重用連接的成本,以及驅動程式是否應登記/取消登記連接(如果該連接要重用連接)。 如果*f 要求事務登記*為 FALSE,驅動程式應忽略*transId*的值。  
  
 驅動程式管理員保證*hRequest*和*h候選連接*的父 HENV 句柄相同。 驅動程式管理員保證與*hRequest*和*h候選連接*關聯的池 ID 相同。  
  
 應用程式不應直接調用此功能。 支援驅動程式感知連接池的ODBC驅動程式必須實現此功能。  
  
 包括用於 ODBC 驅動程式開發的 sqlspi.h。  
  
## <a name="see-also"></a>另請參閱  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [驅動程式感知連接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [在 ODBC 驅動程式中開發連接集區覺察](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
