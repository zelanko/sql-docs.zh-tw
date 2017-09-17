---
title: "設定游標 |Microsoft 文件"
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
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
- cursors [ODBC], creating
ms.assetid: b80afb0e-ef2f-408f-86f5-a392edd99a56
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0e7fda4fa942519384b2837f6f3f70a880dee74f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="setting-up-the-cursor"></a>設定資料指標
應用程式之前執行的陳述式建立的結果集，可以指定資料指標類型。 它會與 的 SQL_ATTR_CURSOR_TYPE 陳述式屬性。 如果應用程式未明確指定型別，就會使用順向資料指標。 若要取得混合的資料指標，指定索引鍵集驅動資料指標的應用程式，但是宣告的索引鍵集大小不超過結果集大小。  
  
 索引鍵集驅動和混合的資料指標，應用程式也可以指定索引鍵集大小。 它會使用 SQL_ATTR_KEYSET_SIZE 陳述式屬性。 如果索引鍵集大小設定為 0，這是預設值，索引鍵集大小設定為結果集大小，且索引鍵集驅動資料指標。 在開啟資料指標之後，就可以變更的索引鍵集大小。  
  
 應用程式也可以設定資料列集大小。如需詳細資訊，請參閱[使用區塊資料指標](../../../odbc/reference/develop-app/using-block-cursors.md)稍早在本章節中。
