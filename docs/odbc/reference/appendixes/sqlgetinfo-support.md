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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a21c035a14814f51d4344894ef253b2cc844f4c2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307799"
---
# <a name="sqlgetinfo-support"></a>SQLGetInfo 支援
當 ODBC 2。*x*應用程式會呼叫**SQLGetInfo**至 ODBC*3.x 驅動程式*，必須支援下表中的*InfoType*引數。  
  
|*InfoType*|傳回值|  
|----------------|-------------|  
|SQL_ALTER_TABLE （ODBC 2.0）**注意：** 此資訊類型未被取代;右側資料行中的位元遮罩已被取代。|SQLINTEGER 位元遮罩，列舉資料來源所支援之**ALTER TABLE**語句中的子句。<br /><br /> 下列位元遮罩是用來決定支援的子句：<br /><br /> SQL_AT_DROP_COLUMN = 支援放置資料行的功能。 這是由驅動程式定義，這會導致 cascade 或 restrict 行為。 （ODBC 2.0）<br /><br /> SQL_AT_ADD_COLUMN = 支援在單一 ALTER TABLE 語句中加入多個資料行的功能。 這個位不會與其他 SQL_AT_ADD_COLUMN_XXX 位或 SQL_AT_CONSTRAINT_XXX 位結合。 （ODBC 2.0）|  
|SQL_FETCH_DIRECTION （ODBC 1.0）<br /><br /> 此資訊類型是在 ODBC 1.0 中引進的;每個位元遮罩都會標示其引進的版本。|SQLINTEGER 位元遮罩，用來列舉支援的 fetch 方向選項。<br /><br /> 下列位元遮罩會與旗標搭配使用，以判斷支援的選項：<br /><br /> SQL_FD_FETCH_NEXT （ODBC 1.0） SQL_FD_FETCH_FIRST （ODBC 1.0） SQL_FD_FETCH_LAST （ODBC 1.0） SQL_FD_FETCH_PRIOR （ODBC 1.0） SQL_FD_FETCH_ABSOLUTE （ODBC 1.0） SQL_FD_FETCH_RELATIVE （ODBC 1.0） SQL_FD_FETCH_BOOKMARK （ODBC 2.0）|  
|SQL_LOCK_TYPES （ODBC 2.0）|SQLINTEGER 位元遮罩，列舉**SQLSetPos**中*fLock*引數支援的鎖定類型。<br /><br /> 下列位元遮罩會與旗標搭配使用，以判斷支援的鎖定類型：<br /><br /> SQL_LCK_NO_CHANGE SQL_LCK_EXCLUSIVE SQL_LCK_UNLOCK|  
|SQL_ODBC_API_CONFORMANCE （ODBC 1.0）|指出 ODBC 一致性層級的 SQLSMALLINT 值。<br /><br /> SQL_OAC_NONE = 無<br /><br /> SQL_OAC_LEVEL1 = 支援層級1<br /><br /> SQL_OAC_LEVEL2 = 支援層級2|  
|SQL_ODBC_SQL_CONFORMANCE （ODBC 1.0）|SQLSMALLINT 值，指出驅動程式支援的 SQL 文法。 如需 SQL 一致性層級的定義，請參閱[附錄 C： Sql 文法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)。<br /><br /> SQL_OSC_MINIMUM = 支援的最低文法<br /><br /> SQL_OSC_CORE = 支援核心文法<br /><br /> SQL_OSC_EXTENDED = 支援的延伸文法|  
|SQL_POS_OPERATIONS （ODBC 2.0）|SQLINTEGER 位元遮罩，列舉**SQLSetPos**中支援的作業。<br /><br /> 下列位元遮罩會與旗標搭配使用，以判斷支援的選項：<br /><br /> SQL_POS_POSITION （ODBC 2.0） SQL_POS_REFRESH （ODBC 2.0） SQL_POS_UPDATE （ODBC 2.0） SQL_POS_DELETE （ODBC 2.0） SQL_POS_ADD （ODBC 2.0）|  
|SQL_POSITIONED_STATEMENTS （ODBC 2.0）|SQLINTEGER 位元遮罩，用來列舉支援的定位 SQL 語句。<br /><br /> 下列位元遮罩是用來決定支援的語句：<br /><br /> SQL_PS_POSITIONED_DELETE SQL_PS_POSITIONED_UPDATE SQL_PS_SELECT_FOR_UPDATE|  
|SQL_SCROLL_CONCURRENCY （ODBC 1.0）|SQLINTEGER 位元遮罩，列舉資料指標所支援的並行控制選項。<br /><br /> 下列位元遮罩是用來決定支援的選項：<br /><br /> SQL_SCCO_READ_ONLY = 資料指標是唯讀的。 不允許任何更新。<br /><br /> SQL_SCCO_LOCK = 資料指標使用的最低層級鎖定足以確保資料列可以更新。<br /><br /> SQL_SCCO_OPT_ROWVER = 資料指標使用開放式並行存取控制，比較資料列版本，例如 SQLBase ROWID 或 Sybase 時間戳記。<br /><br /> SQL_SCCO_OPT_VALUES = 資料指標使用開放式並行存取控制，比較值。|  
|SQL_STATIC_SENSITIVITY （ODBC 2.0）|SQLINTEGER 位元遮罩，用來列舉應用程式透過**SQLSetPos**或定位 update 或 delete 語句所做的變更，是否可由該應用程式偵測到靜態或索引鍵集導向的資料指標。<br /><br /> SQL_SS_ADDITIONS = 已加入的資料列會顯示在資料指標上;游標可以滾動到這些資料列。 將這些資料列加入至資料指標的位置與驅動程式相關。<br /><br /> SQL_SS_DELETIONS = 刪除的資料列無法再供資料指標使用，而且不會在結果集中留下「洞」;資料指標從已刪除的資料列滾動之後，就無法返回該資料列。<br /><br /> SQL_SS_UPDATES = 資料列的更新會顯示在資料指標上;如果資料指標從滾動到已更新的資料列，則游標所傳回的資料就是已更新的資料，而不是原始資料。 此選項只適用于未更新索引鍵的索引鍵集驅動資料指標上的靜態資料指標或更新。 此選項不適用於動態資料指標，或在混合資料指標中變更索引鍵的情況下。<br /><br /> 應用程式是否可以偵測其他使用者對結果集所做的變更（包括相同應用程式中的其他資料指標），取決於資料指標類型。|  
  
 使用 ODBC 3.x*驅動程式的 odbc 3.x 應用程式*不 *.x*應該使用上表所述的*InfoType*引數來呼叫**SQLGetInfo** ，但應該使用下列段落中所列 *.x*的 odbc 3.x *InfoType*引數。 在 ODBC 2 中使用的*InfoType*引數之間沒有一對一的對應關係。*x*和 ODBC 3.x 中使用的 *。* 使用 ODBC 2 的 ODBC*3.x 應用程式。* 另一方面， *x*驅動程式應該使用先前所述的*InfoType*引數。  
  
 上表中的某些資訊類型已被取代，以改用 cursor 屬性資訊類型。 這些已淘汰的資訊類型是 SQL_FETCH_DIRECTION、SQL_LOCK_TYPES、SQL_POS_OPERATIONS、SQL_POSITIONED_STATEMENTS、SQL_SCROLL_CONCURRENCY 和 SQL_STATIC_SENSITIVITY。 新的資料指標屬性類型 SQL_XXX_CURSOR_ATTRIBUTES1and SQL_XXX_CURSOR_ATTRIBUTES2，其中 XXX 等於 DYNAMIC、FORWARD_ONLY、KEYSET_DRIVEN 或 STATIC。 每個新的類型都會指出單一資料指標類型的驅動程式功能。 如需這些選項的詳細資訊，請參閱[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函數描述。
