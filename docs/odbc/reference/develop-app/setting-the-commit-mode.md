---
title: 將認可模式 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
ms.assetid: b60d0d74-0655-4013-8d5a-bc1866eaa166
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e3e3abc5cd7648dce484b6347c30d9290b9fc76a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="setting-the-commit-mode"></a>將認可模式
應用程式會指定連接屬性 SQL_ATTR_AUTOCOMMIT 交易模式。 根據預設，ODBC 異動處於自動認可模式 (除非**SQLSetConnectAttr**和**SQLSetConnectOption**不支援，這是不太可能)。 從手動認可模式切換為自動認可模式自動任何開啟連接上認可交易。
