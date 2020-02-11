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
ms.openlocfilehash: 643d7d4174df66abfcee274c1f987e8f405d19b9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68083337"
---
# <a name="commit-and-rollback-behavior"></a>認可和回復行為
伺服器 Dbms 的常見行為是在認可或回復語句時，關閉資料指標並捨棄備妥的語句。 桌面資料庫更有可能保持開啟資料指標，並保留備妥的語句。 如需詳細資訊，請參閱[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函數描述中的 SQL_CURSOR_COMMIT_BEHAVIOR 和 SQL_CURSOR_ROLLBACK_BEHAVIOR 選項和資料[指標和已備妥之語句上的交易效果](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)。
