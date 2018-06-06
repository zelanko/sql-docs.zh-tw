---
title: 認可和回復行為 |Microsoft 文件
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
- interoperability [ODBC], transaction support
- transactions [ODBC], DBMS support
ms.assetid: 2ac8f012-e46d-41ca-81bb-e4a3246e3241
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d859dcaad175ce7f340ecbf8ad8e08492d22b63c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="commit-and-rollback-behavior"></a>認可和回復行為
Dbms 伺服器之間的共通行為是關閉資料指標，並認可或回復陳述式時，捨棄備妥的陳述式。 桌面的資料庫會更容易將資料指標保持開啟並保持備妥的陳述式。 如需詳細資訊，請參閱 「 SQL_CURSOR_COMMIT_BEHAVIOR 和 SQL_CURSOR_ROLLBACK_BEHAVIOR 選項[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函數描述和[效果的資料指標和備妥的陳述式交易](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md).
