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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68094217"
---
# <a name="setting-the-commit-mode"></a>設定認可模式
應用程式使用 SQL_ATTR_AUTOCOMMIT 連接屬性中指定的交易模式。 根據預設，ODBC 交易處於自動認可模式 (除非**SQLSetConnectAttr**並**SQLSetConnectOption**不支援，這是不太可能)。 從手動認可模式切換至自動認可模式會自動認可任何開啟的交易，在此連接上。
