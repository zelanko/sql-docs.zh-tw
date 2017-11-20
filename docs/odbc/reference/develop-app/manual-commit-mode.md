---
title: "手動認可模式 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- rolling back transactions [ODBC]
- manual-commit mode [ODBC]
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
- transactions [ODBC], rolling back
ms.assetid: 9c4b3931-e48b-4960-89a2-5697537e9f51
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1a5f9d510d1a92ce8faf4fe29f3274afdba6f83b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="manual-commit-mode"></a>手動認可模式
*在手動認可模式下，*應用程式必須明確地完成交易，藉由呼叫**SQLEndTran**認可或復原它們。 這是正常的交易模式，針對大部分的關聯式資料庫。  
  
 ODBC 中的交易並沒有明確初始化。 相反地，在交易開始隱含每當應用程式啟動時在資料庫上運作。 如果資料來源需要明確的交易初始，驅動程式必須提供應用程式執行需要使用交易陳述式，而且沒有目前的交易。

