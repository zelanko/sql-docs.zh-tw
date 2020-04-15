---
title: 返回SQL_NO_DATA |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305109"
---
# <a name="returning-sql_no_data"></a>傳回 SQL_NO_DATA
當使用 ODBC *3.x*驅動程式的 ODBC *2.x*應用程式呼叫**SQLExecDirect、SQLExecute**或**SQLParamData**,並且執行搜尋的更新或刪除語句,但不影響數據源上的任何行時,ODBC *3.x*驅動程式應返回SQL_SUCCESS。 **SQLExecute** 當使用 ODBC *3.x*驅動程式的*3.x*應用程式呼叫**SQLExecDirect、SQLExecute**或**SQLExecute** **SQLParamData**時具有相同的結果,ODBC *3.x*驅動程式應返回SQL_NO_DATA。  
  
 如果一批語句中搜索的更新或刪除語句不會影響數據源中的任何行 **,SQLMore結果**將返回SQL_SUCCESS。 它不能返回SQL_NO_DATA,因為這意味著沒有更多的結果,而不是從搜索的更新/刪除的結果,沒有影響行。
