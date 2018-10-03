---
title: 多個 hstmt （Paradox 驅動程式） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- multiple hstmts [ODBC]
- Paradox driver [ODBC], multiple hstmts
ms.assetid: 66aecd94-092d-43d4-9583-74f5e2990eac
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2dc086f25ca4da2a64a5edde2422f1fe33fcc444
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47626406"
---
# <a name="multiple-hstmts-paradox-driver"></a>多個 hstmt (Paradox 驅動程式)
ODBC Paradox 驅動程式使用時，如果您想要使用多個*hstmt*資料表上執行查詢，資料表必須有唯一的索引 （Paradox 主索引鍵）。
