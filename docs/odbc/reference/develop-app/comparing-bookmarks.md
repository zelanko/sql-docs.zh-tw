---
title: 比較書簽 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], bookmarks
- comparing bookmarks [ODBC]
- bookmarks [ODBC]
ms.assetid: ea347635-fbe3-41c1-b537-4048b7c0f7da
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 44da652ad1e52934fa48f32b1b2f88b30212ad3b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68083298"
---
# <a name="comparing-bookmarks"></a>比較書籤
因為書簽可進行位元組比較，所以可以比較是否相等或不相等。 若要這樣做，應用程式會將每個書簽視為位元組陣列，並逐位元組比較兩個書簽。 因為書簽保證只能在結果集內區分，所以比較從不同結果集取得的書簽並不合理。
