---
title: SQLRowCount |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLRowCount function
ms.assetid: 967ed3d4-3d31-4485-ac92-027076ebc829
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4ff2a744f68cf6152330179eb8dcab1f33911914
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63046603"
---
# <a name="sqlrowcount"></a>SQLRowCount
  當參數值的陣列針對語句執行進行系結`SQLRowCount`時，如果參數值的任何資料列在語句執行時產生錯誤狀況，則會傳回 SQL_ERROR。 函數的*RowCountPtr*引數不會傳回任何值。  
  
 應用程式可以利用 SQL_ATTR_PARAMS_PROCESSED_PTR 陳述式屬性擷取錯誤發生前所處理的參數數目。  
  
 此外，應用程式可以使用透過 SQL_ATTR_PARAM_STATUS_PTR 陳述式屬性繫結的狀態值陣列，擷取衝突參數資料列的陣列位移。 應用程式可以周遊狀態陣列來判斷所處理的資料列實際數目。  
  
 當執行[!INCLUDE[tsql](../../includes/tsql-md.md)]具有 output 子句的 INSERT、UPDATE、DELETE 或 MERGE 語句時，SQLRowCount 將不會傳回受影響的資料列計數，直到 OUTPUT 子句所產生的結果集內的所有資料列都已耗用為止。 若要 sconsume 這些資料列，您可以呼叫 SQLFetch 或 SQLFetchScroll。 SQLResultCols 會傳回-1，直到所有結果資料列都已耗用為止。 在 SQLFetch 或 SQLFetchScroll 傳回 SQL_NO_DATA 之後，應用程式必須呼叫 SQLRowCount 來判斷受影響的資料列數目，再呼叫 SQLMoreResults 以移至下一個結果。  
  
## <a name="see-also"></a>另請參閱  
 [SQLRowCount 函式](https://go.microsoft.com/fwlink/?LinkId=59367)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  
