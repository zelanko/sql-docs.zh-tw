---
title: 步驟 4a： 擷取結果 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], fetching results
- fetches [ODBC], fetching results
ms.assetid: 77d30142-c774-473c-96fb-b364bb92ac60
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 895ee1f657c9f94a3d5a4d1650b2efe3774a8256
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="step-4a-fetch-the-results"></a>步驟 4a： 擷取結果
下一個步驟是擷取結果，如下圖所示。  
  
 ![顯示 ODBC 應用程式的提取結果](../../../odbc/reference/develop-app/media/pr14.gif "pr14")  
  
 如果在 「 步驟 3:: 建置和執行 SQL 陳述式 」 中執行的陳述式**選取**陳述式或類別目錄函式，應用程式會先呼叫**SQLNumResultCols**來判斷資料行的數目在結果集中。 這個步驟並非必要，如果應用程式已經知道設定資料行，例如是硬式編碼的垂直或自訂應用程式中的 SQL 陳述式的結果數目。  
  
 接下來，應用程式擷取名稱、 資料類型、 有效位數和小數位數與每個結果集資料行**SQLDescribeCol**。 同樣地，這不是必要的應用程式，例如已經知道這項資訊的垂直和自訂應用程式。 應用程式傳遞這項資訊來**SQLBindCol**，應用程式變數繫結至結果集的資料行。  
  
 應用程式會立即呼叫**SQLFetch**擷取第一個資料列，並將該資料列的資料放在與繫結的變數**SQLBindCol**。 如果資料列中沒有任何長的資料，然後它會呼叫**SQLGetData**以擷取該資料。 應用程式繼續呼叫**SQLFetch**和**SQLGetData**擷取其他資料。 它已完成擷取資料後，便會呼叫**SQLCloseCursor**來關閉資料指標。  
  
 擷取結果的完整說明，請參閱[擷取結果 （基本）](../../../odbc/reference/develop-app/retrieving-results-basic.md)和[擷取結果 （進階）](../../../odbc/reference/develop-app/retrieving-results-advanced.md)。  
  
 應用程式現在會傳回 「 步驟 3:: 建置和執行 SQL 陳述式 」 執行另一個陳述式中相同的交易。或繼續進行 「 步驟 5:: Commit Transaction"認可或回復交易。
