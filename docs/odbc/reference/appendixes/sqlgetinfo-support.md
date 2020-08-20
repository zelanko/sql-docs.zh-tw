---
description: SQLGetInfo 支援
title: SQLGetInfo 支援 |Microsoft Docs
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
ms.openlocfilehash: cff18a23c7d8c4526fc86904d75375ed5aaaf5a7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471229"
---
# <a name="sqlgetinfo-support"></a>SQLGetInfo 支援
當 ODBC 2 時。*x* 應用程式呼叫 **SQLGetInfo** 至 ODBC 3.x*驅動程式* ，則必須支援下表中的 *InfoType* 引數。  
  
|*InfoType*|傳回|  
|----------------|-------------|  
|SQL_ALTER_TABLE (ODBC 2.0) **注意：**  此資訊類型不會被取代;右側資料行中的位元遮罩已被取代。|SQLINTEGER 位元遮罩，列舉資料來源所支援的 **ALTER TABLE** 語句中的子句。<br /><br /> 下列位元遮罩可用來判斷支援的子句：<br /><br /> SQL_AT_DROP_COLUMN = 支援卸載資料行的功能。 這是否會造成串聯或限制行為為驅動程式定義。  (ODBC 2.0) <br /><br /> SQL_AT_ADD_COLUMN = 支援在單一 ALTER TABLE 語句中加入多個資料行的功能。 此位不會與其他 SQL_AT_ADD_COLUMN_XXX 位或 SQL_AT_CONSTRAINT_XXX 位結合。  (ODBC 2.0) |  
|SQL_FETCH_DIRECTION (ODBC 1.0) <br /><br /> 此資訊類型是在 ODBC 1.0 中引進;每個位元遮罩都會標示其引進的版本。|SQLINTEGER 位元遮罩，可列舉支援的 fetch 方向選項。<br /><br /> 下列位元遮罩可搭配旗標使用，以決定支援的選項：<br /><br /> SQL_FD_FETCH_NEXT (ODBC 1.0) SQL_FD_FETCH_FIRST (ODBC 1.0) SQL_FD_FETCH_LAST (ODBC 1.0) SQL_FD_FETCH_PRIOR (ODBC 1.0) SQL_FD_FETCH_ABSOLUTE (ODBC 1.0) SQL_FD_FETCH_RELATIVE (ODBC 1.0) SQL_FD_FETCH_BOOKMARK (ODBC 2.0) |  
|SQL_LOCK_TYPES (ODBC 2.0) |SQLINTEGER 位元遮罩，列舉**SQLSetPos**中*fLock*引數支援的鎖定類型。<br /><br /> 下列位元遮罩會與旗標一起使用，以判斷支援的鎖定類型：<br /><br /> SQL_LCK_NO_CHANGE SQL_LCK_EXCLUSIVE SQL_LCK_UNLOCK|  
|SQL_ODBC_API_CONFORMANCE (ODBC 1.0) |指出 ODBC 一致性層級的 SQLSMALLINT 值。<br /><br /> SQL_OAC_NONE = None<br /><br /> SQL_OAC_LEVEL1 = 支援層級1<br /><br /> SQL_OAC_LEVEL2 = 支援層級2|  
|SQL_ODBC_SQL_CONFORMANCE (ODBC 1.0) |SQLSMALLINT 值，指出驅動程式支援的 SQL 文法。 請參閱 [附錄 C：](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md) sql 一致性層級定義的 sql 文法。<br /><br /> SQL_OSC_MINIMUM = 支援的最低文法<br /><br /> SQL_OSC_CORE = 核心文法支援<br /><br /> SQL_OSC_EXTENDED = 支援擴充文法|  
|SQL_POS_OPERATIONS (ODBC 2.0) |SQLINTEGER 位元遮罩，列舉 **SQLSetPos**中支援的作業。<br /><br /> 下列位元遮罩可搭配旗標用來判斷支援的選項：<br /><br /> SQL_POS_POSITION (ODBC 2.0) SQL_POS_REFRESH (ODBC 2.0) SQL_POS_UPDATE (ODBC 2.0) SQL_POS_DELETE (ODBC 2.0) SQL_POS_ADD (ODBC 2.0) |  
|SQL_POSITIONED_STATEMENTS (ODBC 2.0) |SQLINTEGER 位元遮罩，可列舉支援的定位 SQL 語句。<br /><br /> 下列位元遮罩可用來判斷支援的語句：<br /><br /> SQL_PS_POSITIONED_DELETE SQL_PS_POSITIONED_UPDATE SQL_PS_SELECT_FOR_UPDATE|  
|SQL_SCROLL_CONCURRENCY (ODBC 1.0) |SQLINTEGER 位元遮罩，可列舉資料指標支援的並行控制選項。<br /><br /> 下列位元遮罩可用來判斷支援的選項：<br /><br /> SQL_SCCO_READ_ONLY = 資料指標是唯讀的。 不允許任何更新。<br /><br /> SQL_SCCO_LOCK = Cursor 最低層級的鎖定就足以確保資料列可以更新。<br /><br /> SQL_SCCO_OPT_ROWVER = Cursor 使用開放式並行存取控制，比較資料列版本，例如 SQLBase ROWID 或 Sybase TIMESTAMP。<br /><br /> SQL_SCCO_OPT_VALUES = 資料指標使用開放式並行存取控制，比較值。|  
|SQL_STATIC_SENSITIVITY (ODBC 2.0) |SQLINTEGER 位元遮罩，可列舉應用程式是否可透過 **SQLSetPos** 或定點更新或 delete 語句，來偵測應用程式對靜態或索引鍵集導向的資料指標所做的變更。<br /><br /> SQL_SS_ADDITIONS = 資料指標可看到加入的資料列;游標可以滾動至這些資料列。 將這些資料列新增至資料指標的位置會與驅動程式相依。<br /><br /> SQL_SS_DELETIONS = 已刪除的資料列無法再用於資料指標，也不會在結果集中留下「洞」;當資料指標從已刪除的資料列中滾動之後，就無法返回該資料列。<br /><br /> SQL_SS_UPDATES = 資料指標可看見資料列的更新;如果資料指標從更新的資料列中滾動並返回，資料指標所傳回的資料就會是更新的資料，而不是原始資料。 此選項只適用于靜態資料指標或未更新索引鍵之索引鍵集驅動資料指標上的更新。 這個選項不適用於動態資料指標，或在混合資料指標中的索引鍵變更時。<br /><br /> 應用程式是否可以偵測其他使用者對結果集所做的變更，包括相同應用程式中的其他資料指標，視資料指標類型而定。|  
  
 使用 ODBC 3.x*驅動程式的 odbc 3.x 應用程式*不 *.x*應使用上表所述的*InfoType*引數來呼叫**SQLGetInfo** ，但應該使用下列段落中所列的 ODBC 3.x *InfoType*自*變數。* 在 ODBC 2 中使用的*InfoType*引數之間不會有一對一的對應關係。*x*和 ODBC 3.x 中使用的 *。* 使用 ODBC 2 的 ODBC*3.x 應用程式。* 另一方面， *x* 驅動程式應該使用先前所述的 *InfoType* 引數。  
  
 上表中的某些資訊類型已被取代，而是使用資料指標屬性資訊類型。 這些已被取代的資訊類型為 SQL_FETCH_DIRECTION、SQL_LOCK_TYPES、SQL_POS_OPERATIONS、SQL_POSITIONED_STATEMENTS、SQL_SCROLL_CONCURRENCY 和 SQL_STATIC_SENSITIVITY。 新的資料指標屬性類型 SQL_XXX_CURSOR_ATTRIBUTES1and SQL_XXX_CURSOR_ATTRIBUTES2，其中 XXX 等於動態、FORWARD_ONLY、KEYSET_DRIVEN 或靜態。 每個新的類型都表示單一資料指標類型的驅動程式功能。 如需這些選項的詳細資訊，請參閱 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 函數描述。
