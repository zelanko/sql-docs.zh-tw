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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036397"
---
# <a name="manual-commit-mode"></a>手動認可模式
*在手動認可模式中，* 應用程式必須藉由呼叫**SQLEndTran**來認可或回復交易，以明確完成交易。 這是大部分關係資料庫的一般交易模式。  
  
 ODBC 中的交易不一定要明確起始。 相反地，每當應用程式在資料庫上啟動作業時，交易就會隱含開始。 如果資料來源需要明確的交易起始，則每當應用程式執行需要交易的語句，而且沒有目前的交易時，驅動程式就必須提供它。
