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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c28392c0d48984b4aaf8a8df442b6a4054a7eced
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307473"
---
# <a name="comparing-bookmarks"></a>比較書籤
因為書簽可進行位元組比較，所以可以比較是否相等或不相等。 若要這樣做，應用程式會將每個書簽視為位元組陣列，並逐位元組比較兩個書簽。 因為書簽保證只能在結果集內區分，所以比較從不同結果集取得的書簽並不合理。
