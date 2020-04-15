---
title: SQLGetStmtAttr |微軟文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLGetStmtAttr function
ms.assetid: e64f4f94-eb73-4477-9745-080b6cbdc751
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f59b7f006387beea3d213b7f120e567487232e69
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282019"
---
# <a name="sqlgetstmtattr"></a>SQLGetStmtAttr
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端ODBC驅動程式擴展SQLGetStmtAttr以公開特定於驅動程式的語句屬性。  
  
 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)列出了同時讀取和寫入的語句屬性。 本主題將列出唯讀的陳述式屬性。  
  
## <a name="sql_sopt_ss_current_command"></a>SQL_SOPT_SS_CURRENT_COMMAND  
 SQL_SOPT_SS_CURRENT_COMMAND 屬性會公開命令批次的目前命令。 傳回值是一個整數，可指定此命令在批次中的位置。 *ValuePtr*值為 SQLLEN 類型。  
  
## <a name="sql_sopt_ss_nocount_status"></a>SQL_SOPT_SS_NOCOUNT_STATUS  
 SQL_SOPT_SS_NOCOUNT_STATUS屬性指示 NOCOUNT 選項的當前設置,該選項[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]控制在調用[SQLRowCount](../../relational-databases/native-client-odbc-api/sqlrowcount.md)時是否報告受語句影響的行數。 *ValuePtr*值為 SQLLEN 類型。  
  
|值|描述|  
|-----------|-----------------|  
|SQL_NC_OFF|NOCOUNT 為 OFF。 SQLRowCount 返回受影響的行數。|  
|SQL_NC_ON|NOCOUNT 為 ON。 SQLRowCount 不會返回受影響的行數,返回的值為 0。|  
  
 如果 SQLRowCount 返回 0,則應用程式應測試SQL_SOPT_SS_NOCOUNT_STATUS。 如果返回SQL_NC_ON,SQLRowCount 中的值 0[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]僅表示 尚未返回行計數。 如果傳回 SQL_NC_OFF，表示 NOCOUNT 是關閉的，而 SQLRowCount 的值為 0 時，表示陳述式沒有影響任何資料列。  
  
 當 SQL_SOPT_SS_NOCOUNT_STATUS 為 SQL_NC_OFF 時，應用程式不應該顯示 SQLRowCount 的值。 大型批次或預存程序可包含多個 SET NOCOUNT 陳述式，因此無法假設 SQL_SOPT_SS_NOCOUNT_STATUS 仍為常數。 每次 SQLRowCount 返回 0 時,都應測試此選項。  
  
## <a name="sql_sopt_ss_querynotification_msgtext"></a>SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT  
 SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT 屬性會傳回查詢通知要求的訊息文字。  
  
## <a name="sqlgetstmtattr-and-table-valued-parameters"></a>SQLGetStmtAttr 和資料表值參數  
 在使用表值參數時,可以調用 SQLGetStmtAttr 來獲取應用程式參數描述符 (APD) 中SQL_SOPT_SS_PARAM_FOCUS的值。 有關SQL_SOPT_SS_PARAM_FOCUS的詳細資訊,請參閱[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)。  
  
 有關表值參數的詳細資訊,請參閱[&#40;ODBC&#41;的表值參數](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLSetStmtAttr 函數](https://go.microsoft.com/fwlink/?LinkId=59370)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
