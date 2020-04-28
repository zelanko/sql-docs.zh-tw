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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ac381024a6b4b67719cb7c098367f63a6176bad0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298188"
---
# <a name="multiple-hstmts-paradox-driver"></a>多個 hstmt (Paradox 驅動程式)
使用 ODBC Paradox 驅動程式時，如果您想要使用一個以上的*hstmt*來執行資料表的查詢，該資料表必須有唯一的索引（Paradox 主鍵）。
