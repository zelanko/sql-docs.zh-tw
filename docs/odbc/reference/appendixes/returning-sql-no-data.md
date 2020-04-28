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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3e2c806edd5d5647e09c00975ad7207ee5c2c876
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305109"
---
# <a name="returning-sql_no_data"></a>傳回 SQL_NO_DATA
當 ODBC 2.x*應用程式**使用 odbc 3.x*驅動程式呼叫**SQLExecDirect**、 **SQLExecute**或**SQLParamData**，且已執行搜尋的 update 或 delete 語句，但不影響資料來源中的任何資料列時 *，ODBC 3.x*驅動程式應該會傳回 SQL_SUCCESS。 使用 ODBC 3.x*驅動程式來*呼叫**SQLExecDirect**、 **SQLExecute**或**SQLParamData**的結果相同時 *，odbc* *3.x 驅動程式*應該會傳回 SQL_NO_DATA。  
  
 如果語句批次中的搜尋 update 或 delete 語句不會影響資料來源中的任何資料列，則**SQLMoreResults**會傳回 SQL_SUCCESS。 它無法傳回 SQL_NO_DATA，因為這表示沒有更多結果，而是搜尋的更新/刪除不影響任何資料列的結果。
