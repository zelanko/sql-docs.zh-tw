---
title: "將認可模式 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
ms.assetid: b60d0d74-0655-4013-8d5a-bc1866eaa166
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 50fbb6064cdf8e36143958d9ef0d6558beeeab21
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="setting-the-commit-mode"></a>將認可模式
應用程式會指定連接屬性 SQL_ATTR_AUTOCOMMIT 交易模式。 根據預設，ODBC 異動處於自動認可模式 (除非**SQLSetConnectAttr**和**SQLSetConnectOption**不支援，這是不太可能)。 從手動認可模式切換為自動認可模式自動任何開啟連接上認可交易。
