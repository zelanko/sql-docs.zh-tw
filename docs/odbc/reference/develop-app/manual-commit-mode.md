---
title: 手動認可模式 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
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
manager: craigg
ms.openlocfilehash: fde932df4d3eaa8e9ae3cceb2f28b6511dfb32d9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="manual-commit-mode"></a>手動認可模式
*在手動認可模式下，*應用程式必須明確地完成交易，藉由呼叫**SQLEndTran**認可或復原它們。 這是正常的交易模式，針對大部分的關聯式資料庫。  
  
 ODBC 中的交易並沒有明確初始化。 相反地，在交易開始隱含每當應用程式啟動時在資料庫上運作。 如果資料來源需要明確的交易初始，驅動程式必須提供應用程式執行需要使用交易陳述式，而且沒有目前的交易。
