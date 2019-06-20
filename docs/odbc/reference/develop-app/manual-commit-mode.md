---
title: 手動認可模式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- rolling back transactions [ODBC]
- manual-commit mode [ODBC]
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
- transactions [ODBC], rolling back
ms.assetid: 9c4b3931-e48b-4960-89a2-5697537e9f51
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1952d4185c80a3b49b7742a9dba1f3d8d41a6ca6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62628909"
---
# <a name="manual-commit-mode"></a>手動認可模式
*在手動認可模式中，* 應用程式必須明確完成的交易，藉由呼叫**SQLEndTran**進行認可或回復它們。 這是大部分的關聯式資料庫的正常的交易模式。  
  
 ODBC 中的交易並沒有明確起始。 相反地，在交易開始隱含每當應用程式啟動時在資料庫上運作。 如果資料來源需要明確的交易起始，此驅動程式必須提供它只要應用程式執行需要使用交易陳述式，且沒有任何目前的交易。
