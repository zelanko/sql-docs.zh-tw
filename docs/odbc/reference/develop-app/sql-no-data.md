---
title: SQL_NO_DATA | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL_NO_DATA [ODBC]
- application upgrades [ODBC], SQL_NO_DATA
- backward compatibility [ODBC], SQL_NO_DATA
- compatibility [ODBC], SQL_NO_DATA
- upgrading applications [ODBC], SQL_NO_DATA
ms.assetid: 07a4144a-a548-4578-b2be-715c3cf73bf8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1f899e7a034e1ec5fc967d834caad3a4ccc4caa1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041828"
---
# <a name="sqlnodata"></a>SQL_NO_DATA
當 ODBC 3。*x*應用程式會呼叫**SQLExecDirect**， **SQLExecute**，或**SQLParamData** ODBC 2。*x*驅動程式來執行搜尋的更新或刪除不會影響在資料來源，此驅動程式的任何資料列的陳述式應傳回 SQL_SUCCESS，不 sql_no_data 為止。 當 ODBC 2。*x*或 ODBC 3。*x*應用程式使用 ODBC 3。*x*驅動程式呼叫**SQLExecDirect**， **SQLExecute**，或**SQLParamData**具有相同的結果，而 ODBC 3。*x*驅動程式應該會傳回 sql_no_data 為止。
