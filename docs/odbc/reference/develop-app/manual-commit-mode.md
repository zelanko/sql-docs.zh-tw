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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2a00ff373e374d0940b3e7259eeb01e26b620cae
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81287872"
---
# <a name="manual-commit-mode"></a>手動認可模式
*在手動認可模式中，* 應用程式必須藉由呼叫**SQLEndTran**來認可或回復交易，以明確完成交易。 這是大部分關係資料庫的一般交易模式。  
  
 ODBC 中的交易不一定要明確起始。 相反地，每當應用程式在資料庫上啟動作業時，交易就會隱含開始。 如果資料來源需要明確的交易起始，則每當應用程式執行需要交易的語句，而且沒有目前的交易時，驅動程式就必須提供它。
