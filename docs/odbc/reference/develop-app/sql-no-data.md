---
title: SQL_NO_DATA |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68041828"
---
# <a name="sql_no_data"></a>SQL_NO_DATA
當 ODBC 3 時。*x*應用程式會呼叫 ODBC 2 中的**SQLExecDirect**、 **SQLExecute**或**SQLParamData** 。*x*驅動程式執行搜尋的 update 或 delete 語句不會影響資料來源中的任何資料列，驅動程式應該會傳回 SQL_SUCCESS，而不是 SQL_NO_DATA。 當 ODBC 2。*x*或 ODBC 3。使用 ODBC 3 的*x*應用程式。*x*驅動程式會以相同的結果（ODBC 3）呼叫**SQLExecDirect**、 **SQLExecute**或**SQLParamData** 。*x*驅動程式應該會傳回 SQL_NO_DATA。
