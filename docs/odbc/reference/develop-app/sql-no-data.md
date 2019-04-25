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
manager: craigg
ms.openlocfilehash: 749351694a41764b9b5cc8bf3421340d62626aaf
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62445960"
---
# <a name="sqlnodata"></a>SQL_NO_DATA
當 ODBC 3。*x*應用程式會呼叫**SQLExecDirect**， **SQLExecute**，或**SQLParamData** ODBC 2。*x*驅動程式來執行搜尋的更新或刪除不會影響在資料來源，此驅動程式的任何資料列的陳述式應傳回 SQL_SUCCESS，不 sql_no_data 為止。 當 ODBC 2。*x*或 ODBC 3。*x*應用程式使用 ODBC 3。*x*驅動程式呼叫**SQLExecDirect**， **SQLExecute**，或**SQLParamData**具有相同的結果，而 ODBC 3。*x*驅動程式應該會傳回 sql_no_data 為止。
