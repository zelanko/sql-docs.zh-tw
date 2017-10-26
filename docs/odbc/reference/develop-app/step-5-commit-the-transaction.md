---
title: "步驟 5： 認可交易 |Microsoft 文件"
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
- application process [ODBC], committing transactions
- committing transactions [ODBC]
- transaction commit [ODBC]
ms.assetid: 311685e2-f7b5-4ddc-8020-59380cd2f035
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9ac53209063a1204b57e7183501b5901dc8ea248
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="step-5-commit-the-transaction"></a>步驟 5： 認可交易
下一個步驟是要認可的交易，在下圖所示。  
  
 ![示範如何將交易認可](../../../odbc/reference/develop-app/media/pr16.gif "pr16")  
  
 第五個步驟是呼叫**SQLEndTran**認可或回復交易。 應用程式執行此步驟中，只有當它設定為手動認可; 的交易認可模式如果交易認可模式為自動認可，這是預設值，會自動認可交易時執行的陳述式。 如需詳細資訊，請參閱[交易](../../../odbc/reference/develop-app/transactions-odbc.md)。  
  
 在新的交易中執行的陳述式，在應用程式會回到步驟 3。 從資料來源中斷連接，應用程式會繼續到步驟 6。

