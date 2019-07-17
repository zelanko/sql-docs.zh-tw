---
title: 步驟 4a：擷取結果 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3ab0bdabe8b2d66bf054f07ea51056a4044b4ae8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114191"
---
# <a name="step-4a-fetch-the-results"></a>步驟 4a：擷取結果
下一步是擷取結果，如下圖所示。  
  
 ![正在擷取 ODBC 應用程式中的結果會顯示](../../../odbc/reference/develop-app/media/pr14.gif "pr14")  
  
 如果陳述式執行，則 「 步驟 3:建置並執行 SQL 陳述式 」 已**選取** 陳述式或類別目錄函式，在應用程式第一次呼叫**SQLNumResultCols**來判斷結果集中的資料行數目。 此步驟不需要應用程式已經知道設定資料行，例如是硬式編碼的垂直或自訂應用程式中的 SQL 陳述式的結果數目。  
  
 接下來，應用程式會擷取名稱、 資料類型、 有效位數和小數位數與每個結果集資料行**SQLDescribeCol**。 同樣地，這不需要熟悉這項資訊的垂直和自訂應用程式等應用程式。 應用程式傳遞這項資訊才能**SQLBindCol**，它會在將應用程式變數中的結果集的資料行繫結。  
  
 應用程式現在會呼叫**SQLFetch**擷取第一個資料列，並將該資料列的資料放在與繫結的變數**SQLBindCol**。 如果資料列中沒有任何長的資料，然後它會呼叫**SQLGetData**以擷取該資料。 若要呼叫的應用程式會繼續**SQLFetch**並**SQLGetData**擷取其他資料。 完成擷取資料之後，它會呼叫**SQLCloseCursor**來關閉資料指標。  
  
 擷取結果的完整說明，請參閱[擷取結果 （基本）](../../../odbc/reference/develop-app/retrieving-results-basic.md)並[擷取結果 （進階）](../../../odbc/reference/develop-app/retrieving-results-advanced.md)。  
  
 應用程式立即返回 「 步驟 3:建置並執行 SQL 陳述式 」 相同的交易; 中執行另一個陳述式或繼續進行 「 步驟 5:認可的交易 」 認可或回復交易。
