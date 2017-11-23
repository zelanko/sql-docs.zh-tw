---
title: "狀態轉換檢查 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- state transition checks [ODBC]
- driver manager [ODBC], error checking
ms.assetid: 0706db7d-e125-4845-a13a-7fe4308f7360
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0d6c33118d108c4a4c9e541db311710202cabdb3
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="state-transition-checks"></a>檢查狀態轉換
驅動程式管理員會檢查環境、 連線或陳述式的狀態是適用於所呼叫的函式。 比方說，連線必須在配置狀態**SQLConnect**呼叫; 陳述式必須在備妥狀態**SQLExecute**呼叫。 驅動程式管理員狀態轉換錯誤會傳回 SQL_ERROR。
