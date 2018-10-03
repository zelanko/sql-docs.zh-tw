---
title: 比較書籤 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 690acf80bfabdc04d5f70b780e41943337c18cb9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47792696"
---
# <a name="comparing-bookmarks"></a>比較書籤
因為位元組比較書籤，它們可以進行相等或不等比較。 若要這樣做，應用程式視為位元組陣列中的每個書籤，然後比較兩個書籤的位元組。 書籤迣窆只在結果集內的不同，因為它沒有意義來比較從不同的結果集所取得的書籤。
