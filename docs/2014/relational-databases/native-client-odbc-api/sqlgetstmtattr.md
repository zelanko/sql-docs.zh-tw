---
title: SQLGetStmtAttr | Microsoft Docs
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
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62657807"
---
# <a name="sqlgetstmtattr"></a>SQLGetStmtAttr
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會擴充 SQLGetStmtAttr 來公開驅動程式特有的陳述式屬性。  
  
 [SQLSetStmtAttr](sqlsetstmtattr.md)清單陳述式屬性，其同時讀取和寫入。 本主題將列出唯讀的陳述式屬性。  
  
## <a name="sqlsoptsscurrentcommand"></a>SQL_SOPT_SS_CURRENT_COMMAND  
 SQL_SOPT_SS_CURRENT_COMMAND 屬性會公開命令批次的目前命令。 傳回值是一個整數，可指定此命令在批次中的位置。 *ValuePtr*的值屬於類型是 SQLLEN。  
  
## <a name="sqlsoptssnocountstatus"></a>SQL_SOPT_SS_NOCOUNT_STATUS  
 SQL_SOPT_SS_NOCOUNT_STATUS 屬性指出 NOCOUNT 的目前設定選項，可控制是否[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]報告的陳述式所影響的資料列數時[SQLRowCount](sqlrowcount.md)呼叫。 *ValuePtr*的值屬於類型是 SQLLEN。  
  
|值|描述|  
|-----------|-----------------|  
|SQL_NC_OFF|NOCOUNT 為 OFF。 SQLRowCount 傳回受影響的資料列數目。|  
|SQL_NC_ON|NOCOUNT 為 ON。 SQLRowCount 不傳回受到影響的資料列數和傳回的值為 0。|  
  
 SQLRowCount 傳回 0，如果應用程式應該測試 SQL_SOPT_SS_NOCOUNT_STATUS。 如果傳回 sql_nc_on，值為 0 時 SQLRowCount 只表示[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]尚未傳回資料列計數。 如果傳回 SQL_NC_OFF，表示 NOCOUNT 是關閉，並從 SQLRowCount 0 的值會指出陳述式並未影響任何資料列。  
  
 當 SQL_SOPT_SS_NOCOUNT_STATUS 為 sql_nc_off 時，應用程式應該不會顯示 SQLRowCount 的值。 大型批次或預存程序可包含多個 SET NOCOUNT 陳述式，因此無法假設 SQL_SOPT_SS_NOCOUNT_STATUS 仍為常數。 此選項應測試每次 SQLRowCount 會傳回 0。  
  
## <a name="sqlsoptssquerynotificationmsgtext"></a>SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT  
 SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT 屬性會傳回查詢通知要求的訊息文字。  
  
## <a name="sqlgetstmtattr-and-table-valued-parameters"></a>SQLGetStmtAttr 和資料表值參數  
 SQLGetStmtAttr 可以呼叫使用資料表值參數時，取得應用程式參數描述項 (APD) 中的 SQL_SOPT_SS_PARAM_FOCUS 值。 如需有關 SQL_SOPT_SS_PARAM_FOCUS 的詳細資訊，請參閱 < [SQLSetStmtAttr](sqlsetstmtattr.md)。  
  
 如需有關資料表值參數的詳細資訊，請參閱 < [Parameters &#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLSetStmtAttr 函數](https://go.microsoft.com/fwlink/?LinkId=59370)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  
