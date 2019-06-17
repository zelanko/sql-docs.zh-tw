---
title: 認可和回復行為 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], transaction support
- transactions [ODBC], DBMS support
ms.assetid: 2ac8f012-e46d-41ca-81bb-e4a3246e3241
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bad1706e7283c0b0a5111e93c9dfd7ae494c8ef4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63125494"
---
# <a name="commit-and-rollback-behavior"></a>認可和回復行為
Dbms 伺服器之間的一般行為是關閉資料指標，並認可或回復陳述式時，捨棄已備妥的陳述式。 桌面資料庫會更容易將資料指標保持開啟，並保留已備妥的陳述式。 如需詳細資訊，請參閱 「 SQL_CURSOR_COMMIT_BEHAVIOR 和 SQL_CURSOR_ROLLBACK_BEHAVIOR 選項[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函式描述和[效果的資料指標和已備妥的陳述式交易](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md).
