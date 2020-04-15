---
title: 第 5 步:提交事務 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e348ce697e512f30db46d14535cf19bd6d530f61
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283348"
---
# <a name="step-5-commit-the-transaction"></a>步驟 5：認可交易
下一步是提交事務,如下圖所示。  
  
 ![顯示如何認可交易](../../../odbc/reference/develop-app/media/pr16.gif "pr16")  
  
 第五步是調用**SQLEndTran**提交或回滾事務。 僅當應用程式將事務提交模式設置為手動提交時,應用程式才會執行此步驟;如果事務提交模式是自動提交(預設值),則在執行語句時會自動提交事務。 如需詳細資訊，請參閱[交易](../../../odbc/reference/develop-app/transactions-odbc.md)。  
  
 要在新事務中執行語句,應用程式將返回到步驟 3。 要斷開與數據源的連接,應用程式將繼續執行步驟 6。
