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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a43a78ad9453f65d9b12595851bd622f720b409a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68094217"
---
# <a name="setting-the-commit-mode"></a>設定認可模式
應用程式會使用 SQL_ATTR_AUTOCOMMIT 連接屬性來指定交易模式。 根據預設，ODBC 交易處於自動認可模式（除非不支援**SQLSetConnectAttr**和**SQLSetConnectOption** ，這不太可能）。 從手動認可模式切換到自動認可模式，會在連接上自動認可任何開啟的交易。
