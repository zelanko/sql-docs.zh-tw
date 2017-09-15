---
title: "步驟 4b： 擷取資料列計數 |Microsoft 文件"
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
- fetches [ODBC], fetching row count
- row count [ODBC]
- application process [ODBC], fetching row count
ms.assetid: 3af481b1-d694-446e-948d-e3a5edcad050
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9b3526d1aad0475cb487f9c1fba6822604286834
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="step-4b-fetch-the-row-count"></a>步驟 4b： 擷取資料列計數
下一個步驟是提取資料列計數，在下圖所示。  
  
 ![顯示提取資料列計數](../../../odbc/reference/develop-app/media/pr15.gif "pr15")  
  
 如果在步驟 3 中執行的陳述式**更新**，**刪除**，或**插入**陳述式中，應用程式擷取受影響的資料列計數**SQLRowCount**。 如需詳細資訊，請參閱[判斷受影響的資料列數目](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)。  
  
 應用程式現在會傳回步驟 3 相同交易中執行另一個陳述式，或繼續進行步驟 5 以認可或回復交易。
