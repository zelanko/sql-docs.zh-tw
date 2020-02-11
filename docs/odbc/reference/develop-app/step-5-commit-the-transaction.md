---
title: 步驟5：認可交易 |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68114134"
---
# <a name="step-5-commit-the-transaction"></a>步驟 5：認可交易
下一個步驟是認可交易，如下圖所示。  
  
 ![顯示如何認可交易](../../../odbc/reference/develop-app/media/pr16.gif "pr16")  
  
 第五個步驟是呼叫**SQLEndTran**來認可或回復交易。 只有當應用程式將交易認可模式設定為手動認可時，才會執行此步驟。如果交易認可模式是自動認可（這是預設值），則會在執行語句時自動認可交易。 如需詳細資訊，請參閱[交易](../../../odbc/reference/develop-app/transactions-odbc.md)。  
  
 若要在新的交易中執行語句，應用程式會回到步驟3。 若要中斷與資料來源的連線，應用程式會繼續進行步驟6。
