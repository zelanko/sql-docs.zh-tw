---
title: "將認可模式 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
ms.assetid: b60d0d74-0655-4013-8d5a-bc1866eaa166
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6d0c38d70b859b1fb986ebaa366a5396159a95da
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="setting-the-commit-mode"></a>將認可模式
應用程式會指定連接屬性 SQL_ATTR_AUTOCOMMIT 交易模式。 根據預設，ODBC 異動處於自動認可模式 (除非**SQLSetConnectAttr**和**SQLSetConnectOption**不支援，這是不太可能)。 從手動認可模式切換為自動認可模式自動任何開啟連接上認可交易。

