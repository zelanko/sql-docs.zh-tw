---
title: SQL_NO_DATA |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL_NO_DATA [ODBC]
- application upgrades [ODBC], SQL_NO_DATA
- backward compatibility [ODBC], SQL_NO_DATA
- compatibility [ODBC], SQL_NO_DATA
- upgrading applications [ODBC], SQL_NO_DATA
ms.assetid: 07a4144a-a548-4578-b2be-715c3cf73bf8
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ff7ba5184642f419a62ffef0610bfc08995ed6b4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sqlnodata"></a>SQL_NO_DATA
當 ODBC 3。*x*應用程式會呼叫**SQLExecDirect**， **SQLExecute**，或**SQLParamData** ODBC 2。*x*執行搜尋的 update 或 delete 陳述式不會影響任何資料列在資料來源，此驅動程式的驅動程式應該會傳回 SQL_SUCCESS，不 sql_no_data 為止。 當 ODBC 2。*x*或 ODBC 3。*x*應用程式使用 ODBC 3。*x*驅動程式呼叫**SQLExecDirect**， **SQLExecute**，或**SQLParamData**具有相同的結果，而 ODBC 3。*x*驅動程式應該會傳回 sql_no_data 為止。
