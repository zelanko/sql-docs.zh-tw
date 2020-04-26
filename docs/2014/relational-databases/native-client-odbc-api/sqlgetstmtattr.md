---
title: SQLGetStmtAttr |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLGetStmtAttr function
ms.assetid: e64f4f94-eb73-4477-9745-080b6cbdc751
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5604aafbbc8a6d77081e829269955c8b7600f4ee
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "62657807"
---
# <a name="sqlgetstmtattr"></a>SQLGetStmtAttr
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驅動程式會擴充 SQLGetStmtAttr，以公開驅動程式特定的語句屬性。  
  
 [SQLSetStmtAttr](sqlsetstmtattr.md)會列出同時為讀取和寫入的語句屬性。 本主題將列出唯讀的陳述式屬性。  
  
## <a name="sql_sopt_ss_current_command"></a>SQL_SOPT_SS_CURRENT_COMMAND  
 SQL_SOPT_SS_CURRENT_COMMAND 屬性會公開命令批次的目前命令。 傳回值是一個整數，可指定此命令在批次中的位置。 *Valueptr 是*值的類型是 SQLLEN。  
  
## <a name="sql_sopt_ss_nocount_status"></a>SQL_SOPT_SS_NOCOUNT_STATUS  
 SQL_SOPT_SS_NOCOUNT_STATUS 屬性工作表示 NOCOUNT 選項的目前設定，其控制是否[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在呼叫[SQLRowCount](sqlrowcount.md)時，報告語句所影響的資料列數目。 *Valueptr 是*值的類型是 SQLLEN。  
  
|值|描述|  
|-----------|-----------------|  
|SQL_NC_OFF|NOCOUNT 為 OFF。 SQLRowCount 會傳回受影響的資料列數目。|  
|SQL_NC_ON|NOCOUNT 為 ON。 SQLRowCount 不會傳回受影響的資料列數目，且傳回的值為0。|  
  
 如果 SQLRowCount 傳回0，應用程式應該測試 SQL_SOPT_SS_NOCOUNT_STATUS。 如果傳回 SQL_NC_ON，則 SQLRowCount 中0的值只會指出[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]尚未傳回資料列計數。 如果傳回 SQL_NC_OFF，表示 NOCOUNT 是關閉的，而 SQLRowCount 的值為 0 時，表示陳述式沒有影響任何資料列。  
  
 當 SQL_SOPT_SS_NOCOUNT_STATUS 為 SQL_NC_OFF 時，應用程式不應該顯示 SQLRowCount 的值。 大型批次或預存程序可包含多個 SET NOCOUNT 陳述式，因此無法假設 SQL_SOPT_SS_NOCOUNT_STATUS 仍為常數。 每次 SQLRowCount 傳回0時，都應該測試此選項。  
  
## <a name="sql_sopt_ss_querynotification_msgtext"></a>SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT  
 SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT 屬性會傳回查詢通知要求的訊息文字。  
  
## <a name="sqlgetstmtattr-and-table-valued-parameters"></a>SQLGetStmtAttr 和資料表值參數  
 使用資料表值參數時，可以呼叫 SQLGetStmtAttr 來取得應用程式參數描述項（APD）中 SQL_SOPT_SS_PARAM_FOCUS 的值。 如需 SQL_SOPT_SS_PARAM_FOCUS 的詳細資訊，請參閱[SQLSetStmtAttr](sqlsetstmtattr.md)。  
  
 如需資料表值參數的詳細資訊，請參閱[ODBC&#41;&#40;的資料表值參數](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLSetStmtAttr 函式](https://go.microsoft.com/fwlink/?LinkId=59370)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  
