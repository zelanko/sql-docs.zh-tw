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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9a399a270eb1cd2f3daf9449c53b1f577a6b9545
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299788"
---
# <a name="sql_no_data"></a>SQL_NO_DATA
當 ODBC 3 時。*x*應用程式會呼叫 ODBC 2 中的**SQLExecDirect**、 **SQLExecute**或**SQLParamData** 。*x*驅動程式執行搜尋的 update 或 delete 語句不會影響資料來源中的任何資料列，驅動程式應該會傳回 SQL_SUCCESS，而不是 SQL_NO_DATA。 當 ODBC 2。*x*或 ODBC 3。使用 ODBC 3 的*x*應用程式。*x*驅動程式會以相同的結果（ODBC 3）呼叫**SQLExecDirect**、 **SQLExecute**或**SQLParamData** 。*x*驅動程式應該會傳回 SQL_NO_DATA。
