---
title: "步驟 3： 建立和執行 SQL 陳述式 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- application process [ODBC], building and executing statements
- SQL statements [ODBC], building and executing
ms.assetid: 133b8bd4-a3c8-4f7e-93c5-c05283c8e96f
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: aa16463daf34d3851a2a1dc214e9f4ba87de6132
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="step-3-build-and-execute-an-sql-statement"></a>步驟 3： 建立和執行 SQL 陳述式
第三個步驟是建置和執行 SQL 陳述式，如下圖所示。 用來執行此步驟的方法很可能會不同極大的差異。 應用程式可能會提示使用者輸入 SQL 陳述式，並建立根據使用者輸入 SQL 陳述式，或使用硬式編碼的 SQL 陳述式。 如需詳細資訊，請參閱[建構 SQL 陳述式](../../../odbc/reference/develop-app/constructing-sql-statements.md)。  
  
 ![建置和執行 SQL 陳述式會顯示](../../../odbc/reference/develop-app/media/pr13.gif "pr13")  
  
 如果 SQL 陳述式包含參數，應用程式繫結至應用程式變數藉由呼叫**SQLBindParameter**每個參數。 如需詳細資訊，請參閱[陳述式參數](../../../odbc/reference/develop-app/statement-parameters.md)。  
  
 使用 SQL 陳述式會建立並繫結任何參數之後，執行陳述式**SQLExecDirect**。 如果陳述式將會執行多次，可以準備使用**SQLPrepare**且與執行**SQLExecute**。 如需詳細資訊，請參閱[執行陳述式](../../../odbc/reference/develop-app/executing-a-statement.md)。  
  
 應用程式可能也會放棄完全執行 SQL 陳述式，並改為呼叫的函式，以傳回結果集包含類別目錄資訊，例如可用的資料行或資料表。 如需詳細資訊，請參閱[的目錄資料會使用](../../../odbc/reference/develop-app/uses-of-catalog-data.md)。  
  
 應用程式的下一個動作，取決於執行 SQL 陳述式類型。  
  
|SQL 陳述式的類型|若要繼續進行|  
|---------------------------|----------------|  
|**選取**或目錄函式|[步驟 4a： 擷取結果](../../../odbc/reference/develop-app/step-4a-fetch-the-results.md)|  
|**更新**，**刪除**，或**插入**|[步驟 4b： 擷取資料列計數](../../../odbc/reference/develop-app/step-4b-fetch-the-row-count.md)|  
|所有其他 SQL 陳述式|步驟 3： 建立和執行 SQL 陳述式 （本主題） 或[步驟 5： 認可交易](../../../odbc/reference/develop-app/step-5-commit-the-transaction.md)|

