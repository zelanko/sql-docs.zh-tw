---
title: 步驟 3： 建置並執行 SQL 陳述式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], building and executing statements
- SQL statements [ODBC], building and executing
ms.assetid: 133b8bd4-a3c8-4f7e-93c5-c05283c8e96f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a3427057e70ee27fe1108fde71c833f0c511836b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47801366"
---
# <a name="step-3-build-and-execute-an-sql-statement"></a>步驟 3：建立和執行 SQL 陳述式
第三個步驟是建置及執行 SQL 陳述式，如下圖所示。 用來執行此步驟的方法很可能極大的差異而有所不同。 應用程式可能會提示使用者輸入 SQL 陳述式，建立根據使用者輸入 SQL 陳述式，或使用硬式編碼的 SQL 陳述式。 如需詳細資訊，請參閱 <<c0> [ 建構 SQL 陳述式](../../../odbc/reference/develop-app/constructing-sql-statements.md)。  
  
 ![建置和執行 SQL 陳述式會顯示](../../../odbc/reference/develop-app/media/pr13.gif "pr13")  
  
 如果 SQL 陳述式包含參數，應用程式將它們繫結至應用程式變數藉由呼叫**SQLBindParameter**每個參數。 如需詳細資訊，請參閱 <<c0> [ 陳述式參數](../../../odbc/reference/develop-app/statement-parameters.md)。  
  
 使用 SQL 陳述式會建立並繫結所有參數之後，執行陳述式**SQLExecDirect**。 如果陳述式將會執行多次，備有**SQLPrepare**且與執行**SQLExecute**。 如需詳細資訊，請參閱 <<c0> [ 執行陳述式](../../../odbc/reference/develop-app/executing-a-statement.md)。  
  
 應用程式可能也放棄完全執行 SQL 陳述式，並改為呼叫的函式，以傳回結果集，其中包含目錄資訊，例如可用的資料行或資料表。 如需詳細資訊，請參閱 <<c0> [ 使用的目錄資料](../../../odbc/reference/develop-app/uses-of-catalog-data.md)。  
  
 應用程式的下一個動作取決於執行 SQL 陳述式的類型。  
  
|SQL 陳述式的類型|請繼續進行|  
|---------------------------|----------------|  
|**選取**或目錄函式|[步驟 4a：擷取結果](../../../odbc/reference/develop-app/step-4a-fetch-the-results.md)|  
|**更新**，**刪除**，或**插入**|[步驟 4b：擷取資料列計數](../../../odbc/reference/develop-app/step-4b-fetch-the-row-count.md)|  
|所有其他 SQL 陳述式|步驟 3： 建置並執行 SQL 陳述式 （本主題） 或[步驟 5： 認可交易](../../../odbc/reference/develop-app/step-5-commit-the-transaction.md)|
