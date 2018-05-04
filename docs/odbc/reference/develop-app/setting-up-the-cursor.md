---
title: 設定游標 |Microsoft 文件
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
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
- cursors [ODBC], creating
ms.assetid: b80afb0e-ef2f-408f-86f5-a392edd99a56
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a7261481c5d484f3cff774b00e0318432c0e085d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="setting-up-the-cursor"></a>設定資料指標
應用程式之前執行的陳述式建立的結果集，可以指定資料指標類型。 它會與 的 SQL_ATTR_CURSOR_TYPE 陳述式屬性。 如果應用程式未明確指定型別，就會使用順向資料指標。 若要取得混合的資料指標，指定索引鍵集驅動資料指標的應用程式，但是宣告的索引鍵集大小不超過結果集大小。  
  
 索引鍵集驅動和混合的資料指標，應用程式也可以指定索引鍵集大小。 它會使用 SQL_ATTR_KEYSET_SIZE 陳述式屬性。 如果索引鍵集大小設定為 0，這是預設值，索引鍵集大小設定為結果集大小，且索引鍵集驅動資料指標。 在開啟資料指標之後，就可以變更的索引鍵集大小。  
  
 應用程式也可以設定資料列集大小。如需詳細資訊，請參閱[使用區塊資料指標](../../../odbc/reference/develop-app/using-block-cursors.md)稍早在本章節中。
