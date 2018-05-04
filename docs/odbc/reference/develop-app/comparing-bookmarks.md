---
title: 比較的書籤 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], bookmarks
- comparing bookmarks [ODBC]
- bookmarks [ODBC]
ms.assetid: ea347635-fbe3-41c1-b537-4048b7c0f7da
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 05d1d66c7eec8f1e02d4195a6bf09d35c3d28203
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="comparing-bookmarks"></a>比較的書籤
因為位元組比較書籤，他們可以針對相等或不等比較。 若要這樣做，應用程式視為一個位元組陣列的每個書籤，然後比較兩個書籤的位元組。 書籤都保證會是只在結果集內的不同，因為它有意義沒有比較從不同的結果集所取得的書籤。
