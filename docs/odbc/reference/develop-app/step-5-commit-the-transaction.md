---
title: 步驟 5： 認可交易 |Microsoft 文件
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
- application process [ODBC], committing transactions
- committing transactions [ODBC]
- transaction commit [ODBC]
ms.assetid: 311685e2-f7b5-4ddc-8020-59380cd2f035
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9e5bf6aa16444a2a2151102ebf31fb45e0f8edb3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="step-5-commit-the-transaction"></a>步驟 5： 認可交易
下一個步驟是要認可的交易，在下圖所示。  
  
 ![示範如何將交易認可](../../../odbc/reference/develop-app/media/pr16.gif "pr16")  
  
 第五個步驟是呼叫**SQLEndTran**認可或回復交易。 應用程式執行此步驟中，只有當它設定為手動認可; 的交易認可模式如果交易認可模式為自動認可，這是預設值，會自動認可交易時執行的陳述式。 如需詳細資訊，請參閱[交易](../../../odbc/reference/develop-app/transactions-odbc.md)。  
  
 在新的交易中執行的陳述式，在應用程式會回到步驟 3。 從資料來源中斷連接，應用程式會繼續到步驟 6。
