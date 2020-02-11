---
title: 步驟3：建立和執行 SQL 語句 |Microsoft Docs
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
ms.openlocfilehash: f0e369b74ef629c5fd7136b9098f579b5ad2b1b4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68114256"
---
# <a name="step-3-build-and-execute-an-sql-statement"></a>步驟 3：建立和執行 SQL 陳述式
第三個步驟是建立並執行 SQL 語句，如下圖所示。 用來執行此步驟的方法可能會有極大的差異。 應用程式可能會提示使用者輸入 SQL 語句、根據使用者輸入建立 SQL 語句，或使用硬式編碼的 SQL 語句。 如需詳細資訊，請參閱[建立 SQL 語句](../../../odbc/reference/develop-app/constructing-sql-statements.md)。  
  
 ![顯示 SQL 陳述式的建置和執行](../../../odbc/reference/develop-app/media/pr13.gif "pr13")  
  
 如果 SQL 語句包含參數，應用程式會藉由呼叫每個參數的**SQLBindParameter** ，將它們系結至應用程式變數。 如需詳細資訊，請參閱[語句參數](../../../odbc/reference/develop-app/statement-parameters.md)。  
  
 在建立 SQL 語句並系結任何參數之後，就會使用**SQLExecDirect**來執行語句。 如果語句會多次執行，它可以使用**SQLPrepare**來準備，並使用**SQLExecute**來執行。 如需詳細資訊，請參閱[執行語句](../../../odbc/reference/develop-app/executing-a-statement.md)。  
  
 應用程式可能也會放棄執行 SQL 語句，而改為呼叫函數來傳回包含目錄資訊的結果集，例如可用的資料行或資料表。 如需詳細資訊，請參閱[目錄資料的使用](../../../odbc/reference/develop-app/uses-of-catalog-data.md)。  
  
 應用程式的下一個動作取決於所執行的 SQL 語句類型。  
  
|SQL 語句的類型|繼續進行|  
|---------------------------|----------------|  
|**選取**或類別目錄函式|[步驟 4a：擷取結果](../../../odbc/reference/develop-app/step-4a-fetch-the-results.md)|  
|**更新**、**刪除**或**插入**|[步驟 4b：擷取資料列計數](../../../odbc/reference/develop-app/step-4b-fetch-the-row-count.md)|  
|所有其他 SQL 語句|步驟3：建立和執行 SQL 語句（本主題）或[步驟5：認可交易](../../../odbc/reference/develop-app/step-5-commit-the-transaction.md)|
