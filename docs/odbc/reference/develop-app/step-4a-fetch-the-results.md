---
title: 步驟4a：提取結果 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], fetching results
- fetches [ODBC], fetching results
ms.assetid: 77d30142-c774-473c-96fb-b364bb92ac60
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c4f810e5c42b54ec871c233ab498936abae610dc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302969"
---
# <a name="step-4a-fetch-the-results"></a>步驟 4a：擷取結果
下一個步驟是提取結果，如下圖所示。  
  
 ![顯示 ODBC 應用程式的提取結果](../../../odbc/reference/develop-app/media/pr14.gif "pr14")  
  
 如果在「步驟3：建立和執行 SQL 語句」中執行的語句是**SELECT**語句或目錄函式，則應用程式會先呼叫**SQLNumResultCols**來判斷結果集中的資料行數目。 如果應用程式已經知道結果集資料行的數目，例如在垂直或自訂應用程式中將 SQL 語句硬式編碼，就不需要這個步驟。  
  
 接下來，應用程式會使用**SQLDescribeCol**來抓取每個結果集資料行的名稱、資料類型、有效位數和小數位數。 同樣地，應用程式（例如，已知道這類資訊的垂直和自訂應用程式）並不需要這麼做。 應用程式會將這項資訊傳遞給**SQLBindCol**，這會將應用程式變數系結至結果集內的資料行。  
  
 應用程式現在會呼叫**SQLFetch**來取出第一個資料列，並將該資料列中的資料放在與**SQLBindCol**系結的變數中。 如果資料列中有任何長整數，則會呼叫**SQLGetData**來取得該資料。 應用程式會繼續呼叫**SQLFetch**和**SQLGetData** ，以取得其他資料。 完成提取資料之後，它會呼叫**SQLCloseCursor**來關閉資料指標。  
  
 如需抓取結果的完整描述，請參閱抓取[結果（基本）](../../../odbc/reference/develop-app/retrieving-results-basic.md)和抓取[結果（Advanced）](../../../odbc/reference/develop-app/retrieving-results-advanced.md)。  
  
 應用程式現在會回到「步驟3：建立並執行 SQL 語句」，以在相同的交易中執行另一個語句;或是繼續進行「步驟5：認可交易」來認可或回復交易。
