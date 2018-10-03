---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6eb6bedb20e1f61c48776d03df59aa6865cfb2a3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47680776"
---
# <a name="sqlgetinfo-support"></a>SQLGetInfo 支援
當 ODBC 2。*x*應用程式會呼叫**SQLGetInfo** ODBC 3 *.x*驅動程式*資訊類型*必須支援下表中的引數。  
  
|*資訊類型*|傳回值|  
|----------------|-------------|  
|(ODBC 2.0) SQL_ALTER_TABLE**附註：** 此資訊類型未被取代; 已被取代的右邊資料行中的位元遮罩。|列舉中的子句 SQLINTEGER 位元遮罩**ALTER TABLE**資料來源所支援的陳述式。<br /><br /> 下列的位元遮罩用來判斷支援哪些子句：<br /><br /> SQL_AT_DROP_COLUMN = 支援卸除資料行的能力。 這會導致 cascade 還是限制行為是由驅動程式定義。 ODBC (2.0)<br /><br /> SQL_AT_ADD_COLUMN = 新增支援在單一的 ALTER TABLE 陳述式中的多個資料行的能力。 此位元不能與其他 SQL_AT_ADD_COLUMN_XXX 位元或 SQL_AT_CONSTRAINT_XXX 位元合併。 ODBC (2.0)|  
|SQL_FETCH_DIRECTION (ODBC 1.0)<br /><br /> ODBC 1.0; 中導入的資訊類型它引進的版本會標示每一個位元遮罩。|SQLINTEGER 位元遮罩列舉支援的提取方向選項。<br /><br /> 下列的位元遮罩與旗標搭配用於決定支援的選項：<br /><br /> SQL_FD_FETCH_NEXT (ODBC 1.0) SQL_FD_FETCH_FIRST (ODBC 1.0) SQL_FD_FETCH_LAST (ODBC 1.0) SQL_FD_FETCH_PRIOR (ODBC 1.0) SQL_FD_FETCH_ABSOLUTE (ODBC 1.0) SQL_FD_FETCH_RELATIVE (ODBC 1.0) SQL_FD_FETCH_BOOKMARK (ODBC 2.0)|  
|SQL_LOCK_TYPES (ODBC 2.0)|列舉支援的鎖定 SQLINTEGER 位元遮罩類型*fLock*中的引數**SQLSetPos**。<br /><br /> 下列的位元遮罩可搭配旗標來判斷支援哪些鎖定類型：<br /><br /> SQL_LCK_NO_CHANGE SQL_LCK_EXCLUSIVE SQL_LCK_UNLOCK|  
|SQL_ODBC_API_CONFORMANCE (ODBC 1.0)|SQLSMALLINT 值，表示 ODBC 一致性層級。<br /><br /> SQL_OAC_NONE = 無<br /><br /> SQL_OAC_LEVEL1 = 支援的層級 1<br /><br /> SQL_OAC_LEVEL2 = 層級 2 支援|  
|SQL_ODBC_SQL_CONFORMANCE (ODBC 1.0)|SQLSMALLINT 值，指出驅動程式支援的 SQL 文法。 請參閱[附錄 c: SQL 文法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)SQL 一致性層級的定義。<br /><br /> SQL_OSC_MINIMUM = 支援的最小文法<br /><br /> SQL_OSC_CORE = 支援的核心文法<br /><br /> SQL_OSC_EXTENDED = 支援的延伸文法|  
|SQL_POS_OPERATIONS (ODBC 2.0)|列舉中支援的作業 SQLINTEGER 位元遮罩**SQLSetPos**。<br /><br /> 下列的位元遮罩用來搭配旗標來判斷支援哪些選項：<br /><br /> SQL_POS_POSITION (ODBC 2.0) SQL_POS_REFRESH (ODBC 2.0) SQL_POS_UPDATE (ODBC 2.0) SQL_POS_DELETE (ODBC 2.0) SQL_POS_ADD (ODBC 2.0)|  
|SQL_POSITIONED_STATEMENTS (ODBC 2.0)|列舉支援 SQLINTEGER 位元遮罩定點的 SQL 陳述式。<br /><br /> 下列的位元遮罩用來判斷支援哪些陳述式：<br /><br /> SQL_PS_POSITIONED_DELETE SQL_PS_POSITIONED_UPDATE SQL_PS_SELECT_FOR_UPDATE|  
|SQL_SCROLL_CONCURRENCY (ODBC 1.0)|SQLINTEGER 位元遮罩列舉支援的資料指標的並行控制選項。<br /><br /> 下列的位元遮罩用來判斷支援哪些選項：<br /><br /> SQL_SCCO_READ_ONLY = 資料指標是唯讀的。 不允許任何更新。<br /><br /> SQL_SCCO_LOCK = 資料指標會使用鎖定不足以確保可以更新資料列的最低層級。<br /><br /> SQL_SCCO_OPT_ROWVER = 資料指標使用開放式並行存取控制，比較資料列版本，例如 SQLBase ROWID 或 Sybase 時間戳記。<br /><br /> SQL_SCCO_OPT_VALUES = 資料指標使用開放式並行存取控制，比較值。|  
|SQL_STATIC_SENSITIVITY (ODBC 2.0)|SQLINTEGER 位元遮罩，列舉應用程式透過靜態或索引鍵集驅動資料指標所做的變更是否**SQLSetPos**或定位的 update 或 delete 陳述式可以偵測到該應用程式。<br /><br /> SQL_SS_ADDITIONS = 新增資料列會顯示資料指標;這些資料列可以捲動資料指標。 其中將這些資料列加入至游標處會驅動程式而異。<br /><br /> SQL_SS_DELETIONS = 已刪除資料列便無法再使用資料指標並不會讓結果集; 中的 「 漏洞 」從已刪除的資料列的資料指標捲動之後，就無法返回該資料列。<br /><br /> SQL_SS_UPDATES = 更新資料列會顯示資料指標;如果資料指標從捲動，並傳回更新的資料列，資料指標所傳回的資料是更新的資料，而不是原始的資料。 此選項會套用為靜態資料指標或更新不會更新索引鍵的索引鍵集驅動資料指標。 此選項不適用於動態資料指標，或在案例中混合資料指標中變更金鑰時在其中。<br /><br /> 應用程式是否可以偵測到結果集由其他使用者，在相同的應用程式，包括其他資料指標所做的變更取決於資料指標類型。|  
  
 ODBC 3 *.x*應用程式使用 ODBC 3 *.x*驅動程式不應該呼叫**SQLGetInfo**具有*資訊類型*引數中所述上述資料表，但應該使用 ODBC 3 *.x* *資訊類型*下列段落中列出的引數。 不是一對一*資訊類型*ODBC 2 中所使用的引數。*x*與所用的 ODBC 3 *.x*。 ODBC 3 *.x*應用程式使用 ODBC 2。*x*驅動程式，相反地，應該使用*資訊類型*先前所述的引數。  
  
 上表中的資訊類型的一些已取代為資料指標屬性的資訊類型。 這些被取代的類型為 SQL_FETCH_DIRECTION、 SQL_LOCK_TYPES、 SQL_POS_OPERATIONS、 SQL_POSITIONED_STATEMENTS、 SQL_SCROLL_CONCURRENCY，以及 SQL_STATIC_SENSITIVITY 的資訊。 新的資料指標屬性類型是 SQL_XXX_CURSOR_ATTRIBUTES1and SQL_XXX_CURSOR_ATTRIBUTES2，其中 XXX 等於動態、 FORWARD_ONLY、 KEYSET_DRIVEN 或靜態。 每個新的型別表示單一的資料指標類型的驅動程式功能。 如需這些選項的詳細資訊，請參閱[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函式描述。
