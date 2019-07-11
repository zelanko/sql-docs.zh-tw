---
title: 傳回 SQL_NO_DATA |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL_NO_DATA [ODBC]
- backward compatibility [ODBC], SQL_NO_DATA
- compatibility [ODBC], SQL_NO_DATA
ms.assetid: deed0163-9d1a-4e9b-9342-3f82e64477d2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e2f731589dcbc10d24ff42d895db60f9f8c054de
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2019
ms.locfileid: "67794176"
---
# <a name="returning-sqlnodata"></a>傳回 SQL_NO_DATA
當 ODBC *2.x*應用程式使用 ODBC *3.x*驅動程式呼叫**SQLExecDirect**， **SQLExecute**，或**SQLParamData**，並搜尋的 update 或 delete 陳述式執行，但不是會影響任何資料列，在資料來源，ODBC *3.x*驅動程式應該會傳回 SQL_SUCCESS。 當 ODBC *3.x*應用程式使用 ODBC *3.x*驅動程式呼叫**SQLExecDirect**， **SQLExecute**，或**SQLParamData**得到相同的結果，而 ODBC *3.x*驅動程式應該會傳回 sql_no_data 為止。  
  
 如果搜尋的 update 或 delete 陳述式在批次陳述式不會影響資料來源，在任何資料列**SQLMoreResults**都會傳回 SQL_SUCCESS。 它不能傳回 sql_no_data 之後，，因為這可能表示有沒有更多的結果，不會有也是從搜尋的更新/刪除，受影響的任何資料列的結果。
