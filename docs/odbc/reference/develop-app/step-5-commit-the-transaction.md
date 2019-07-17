---
title: 步驟 5：認可的交易 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], committing transactions
- committing transactions [ODBC]
- transaction commit [ODBC]
ms.assetid: 311685e2-f7b5-4ddc-8020-59380cd2f035
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bde493edbc6d677b27ef72a24736b504959a7b59
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114134"
---
# <a name="step-5-commit-the-transaction"></a>步驟 5：認可交易
下一個步驟是認可交易，如下圖所示。  
  
 ![示範如何將交易認可](../../../odbc/reference/develop-app/media/pr16.gif "pr16")  
  
 第五個步驟是呼叫**SQLEndTran**認可或回復交易。 應用程式執行此步驟中，只有當它設定為手動認可; 的交易認可模式如果異動認可模式為自動認可，也就是預設值，會自動認可交易中執行的陳述式。 如需詳細資訊，請參閱 <<c0> [ 交易](../../../odbc/reference/develop-app/transactions-odbc.md)。  
  
 在新的交易中執行的陳述式，應用程式會回到步驟 3。 若要從資料來源中斷連線，應用程式會繼續進行步驟 6。
