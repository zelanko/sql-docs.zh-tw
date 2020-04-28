---
title: 設定認可模式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
ms.assetid: b60d0d74-0655-4013-8d5a-bc1866eaa166
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f05aaca2349a612cda7c5b6b257e7a1d5a5ea9c5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299818"
---
# <a name="setting-the-commit-mode"></a>設定認可模式
應用程式會使用 SQL_ATTR_AUTOCOMMIT 連接屬性來指定交易模式。 根據預設，ODBC 交易處於自動認可模式（除非不支援**SQLSetConnectAttr**和**SQLSetConnectOption** ，這不太可能）。 從手動認可模式切換到自動認可模式，會在連接上自動認可任何開啟的交易。
