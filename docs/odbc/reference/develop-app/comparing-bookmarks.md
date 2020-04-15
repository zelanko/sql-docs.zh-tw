---
title: 比較書籤 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307473"
---
# <a name="comparing-bookmarks"></a>比較書籤
由於書籤是位元組可比的,因此可以比較它們對於相等或不等式。 為此,應用程式將每個書籤視為位元組,並逐位元組比較兩個書簽位元組。 由於書籤保證僅在結果集中中不同,因此比較從不同結果集獲得的書籤是沒有意義的。
