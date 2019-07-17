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
ms.openlocfilehash: 7189a0586ba4f62091d5eb209a56931627bc6f7f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036397"
---
# <a name="manual-commit-mode"></a>手動認可模式
*在手動認可模式中，* 應用程式必須明確完成的交易，藉由呼叫**SQLEndTran**進行認可或回復它們。 這是大部分的關聯式資料庫的正常的交易模式。  
  
 ODBC 中的交易並沒有明確起始。 相反地，在交易開始隱含每當應用程式啟動時在資料庫上運作。 如果資料來源需要明確的交易起始，此驅動程式必須提供它只要應用程式執行需要使用交易陳述式，且沒有任何目前的交易。
