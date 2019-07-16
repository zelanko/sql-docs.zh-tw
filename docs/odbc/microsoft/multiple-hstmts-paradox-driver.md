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
ms.openlocfilehash: 5e7a9a4ec0d6426779fb55d923bc7f0607089aad
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68045027"
---
# <a name="multiple-hstmts-paradox-driver"></a>多個 hstmt (Paradox 驅動程式)
ODBC Paradox 驅動程式使用時，如果您想要使用多個*hstmt*資料表上執行查詢，資料表必須有唯一的索引 （Paradox 主索引鍵）。
