---
title: 提交和回滾行為 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c67c29b295160a2908152b22c7a349ce4c0f9f50
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299128"
---
# <a name="commit-and-rollback-behavior"></a>認可和回復行為
伺服器 DBMS 之間的常見行為是在提交或回滾語句時關閉游標並丟棄準備好的語句。 桌面資料庫更有可能保持游標打開並保持準備好的語句。 有關詳細資訊,請參閱[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函數描述中SQL_CURSOR_COMMIT_BEHAVIOR和SQL_CURSOR_ROLLBACK_BEHAVIOR選項以及[事務對游標和準備敘述的影響](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)。
