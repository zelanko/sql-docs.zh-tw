---
title: SQLGetInfo 支援 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], SQLGetInfo
- backward compatibility [ODBC], SQLGetInfo
- SQLGetInfo function [ODBC], support
ms.assetid: 57326f57-daba-46b6-b0be-6c97213b9ef1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a21c035a14814f51d4344894ef253b2cc844f4c2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307799"
---
# <a name="sqlgetinfo-support"></a>SQLGetInfo 支援
當一個ODBC 2。*x*應用程式將**SQLGetInfo**呼叫 ODBC 3 *.x*驅動程式,必須支援下表中的*InfoType*參數。  
  
|*資訊類型*|傳回值|  
|----------------|-------------|  
|SQL_ALTER_TABLE (ODBC 2.0)**注意:** 此資訊類型不會棄用;右側列中的位掩碼被棄用。|SQLINTEGER 位掩碼,枚舉數據來源支援的**ALTER TABLE**語句中子句。<br /><br /> 以下位遮罩用於確定哪些子句受支援:<br /><br /> SQL_AT_DROP_COLUMN = 支援刪除欄的功能。 這是否導致級聯或限制行為是驅動程式定義的。 (ODBC 2.0)<br /><br /> SQL_AT_ADD_COLUMN = 支援在單個 ALTER TABLE 語句中添加多列的功能。 此位不與其他SQL_AT_ADD_COLUMN_XXX位或SQL_AT_CONSTRAINT_XXX位組合。 (ODBC 2.0)|  
|SQL_FETCH_DIRECTION (ODBC 1.0)<br /><br /> ODBC 1.0 中引入了信息類型;每個位掩碼都標有引入它的版本。|SQLINTEGER 位掩碼枚舉了支援的提取方向選項。<br /><br /> 以下位遮罩與標誌結合使用,以確定支援哪些選項:<br /><br /> SQL_FD_FETCH_NEXT (ODBC 1.0) SQL_FD_FETCH_FIRST (ODBC 1.0) SQL_FD_FETCH_LAST (ODBC 1.0) SQL_FD_FETCH_PRIOR (ODBC 1.0) SQL_FD_FETCH_ABSOLUTE (ODBC 1.0) SQL_FD_FETCH_RELATIVE (ODBC 1.0) SQL_FD_FETCH_BOOKMARK (ODBC 2.0)|  
|SQL_LOCK_TYPES (ODBC 2.0)|SQLINTEGER 位罩,枚舉**SQLSetPos***中 fLock*參數支援的鎖類型。<br /><br /> 以下位遮罩與標誌結合使用,以確定支援哪些鎖類型:<br /><br /> SQL_LCK_NO_CHANGESQL_LCK_EXCLUSIVESQL_LCK_UNLOCK|  
|SQL_ODBC_API_CONFORMANCE (ODBC 1.0)|指示 ODBC 符合性級別的 SQLSMALLINT 值。<br /><br /> SQL_OAC_NONE = 無<br /><br /> SQL_OAC_LEVEL1 = 支援等級 1<br /><br /> SQL_OAC_LEVEL2 = 支援 2 級|  
|SQL_ODBC_SQL_CONFORMANCE (ODBC 1.0)|指示驅動程式支援的 SQL 語法的 SQLSMALLINT 值。 有關 SQL 符合性層級定義,請參閱[附錄 C:SQL 語法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)。<br /><br /> SQL_OSC_MINIMUM = 支援最小文法<br /><br /> SQL_OSC_CORE = 支援核心語法<br /><br /> SQL_OSC_EXTENDED = 支援延伸文法|  
|SQL_POS_OPERATIONS (ODBC 2.0)|在**SQLSetPos**中枚舉受支援的操作的 SQLINTEGER 位遮罩。<br /><br /> 以下位遮罩用於與標誌結合,以確定支援哪些選項:<br /><br /> SQL_POS_POSITION (ODBC 2.0) SQL_POS_REFRESH (ODBC 2.0) SQL_POS_UPDATE (ODBC 2.0) SQL_POS_DELETE (ODBC 2.0) SQL_POS_ADD (ODBC 2.0)|  
|SQL_POSITIONED_STATEMENTS (ODBC 2.0)|枚舉支援的 SQL 語句的 SQLINTEGER 位掩碼。<br /><br /> 以下位遮罩支援哪些語句:<br /><br /> SQL_PS_POSITIONED_DELETE SQL_PS_POSITIONED_UPDATE SQL_PS_SELECT_FOR_UPDATE|  
|SQL_SCROLL_CONCURRENCY (ODBC 1.0)|一個 SQLINTEGER 位掩碼,枚舉游標支援的併發控制選項。<br /><br /> 以下位遮罩要決定哪些選項受支援:<br /><br /> SQL_SCCO_READ_ONLY = 游標是唯讀的。 不允許更新。<br /><br /> SQL_SCCO_LOCK = Cursor 使用盡可能低的鎖定級別來確保可以更新行。<br /><br /> SQL_SCCO_OPT_ROWVER = 游標使用樂觀併發控制,比較行版本,如 SQLBase ROWID 或 Sybase TIMESTAMP。<br /><br /> SQL_SCCO_OPT_VALUES = 游標使用樂觀併發控制,比較值。|  
|SQL_STATIC_SENSITIVITY (ODBC 2.0)|SQLINTEGER 位掩碼枚舉,該應用程式是否可以檢測到應用程式通過**SQLSetPos**對靜態或按鍵集驅動的游標所做的更改,或者該應用程式是否可以檢測到定位的更新或刪除語句。<br /><br /> SQL_SS_ADDITIONS = 添加的行對游標可見;游標可以滾動到這些行。 將這些行添加到游標的位置與驅動程序相關。<br /><br /> SQL_SS_DELETIONS = 刪除的行不再可用於游標,也不會在結果集中留下"孔";游標從已刪除的行滾動后,無法返回到該行。<br /><br /> SQL_SS_UPDATES = 對行的更新對游標可見;如果游標從中滾動並返回到更新的行,則游標返回的數據是更新的數據,而不是原始數據。 此選項僅適用於不更新密鑰的鍵集驅動的游標上的靜態游標或更新。 此選項不適用於動態游標,也不適用於在混合游標中更改鍵的情況。<br /><br /> 應用程式是否可以檢測其他使用者(包括同一應用程式中的其他游標)對結果集所做的更改,取決於游標類型。|  
  
 使用 ODBC 3 *.x*驅動程式的 ODBC 3 *.x*應用程式不應使用上表中描述的*InfoType*參數呼叫**SQLGetInfo,** 而應使用下一段中列出的 ODBC 3 *.x* *InfoType*參數。 ODBC 2 中使用的*InfoType*參數之間沒有一對一的對應關係。*x*和 ODBC 3 *.x*中使用的。 與 ODBC 2 配合使用的 ODBC 3 *.x*應用程式。*另一方面,x*驅動程式應使用前面介紹*的 InfoType*參數。  
  
 上表中的某些信息類型被棄用,而傾向於游標屬性信息類型。 這些棄用的信息類型SQL_FETCH_DIRECTION、SQL_LOCK_TYPES、SQL_POS_OPERATIONS、SQL_POSITIONED_STATEMENTS、SQL_SCROLL_CONCURRENCY和SQL_STATIC_SENSITIVITY。 新的遊標屬性類型SQL_XXX_CURSOR_ATTRIBUTES1andSQL_XXX_CURSOR_ATTRIBUTES2,其中 XXX 等於 DYNAMIC、FORWARD_ONLY、KEYSET_DRIVEN 或 STATIC。 每種新類型都表示單個游標類型的驅動程式功能。 有關這些選項的詳細資訊,請參閱[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函數說明。
