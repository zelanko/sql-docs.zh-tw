---
title: 設定資料指標 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
- cursors [ODBC], creating
ms.assetid: b80afb0e-ef2f-408f-86f5-a392edd99a56
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 59ade343f282933e05619996b119bc08e2dfb2ab
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62445910"
---
# <a name="setting-up-the-cursor"></a>設定資料指標
應用程式之前執行的陳述式，建立結果集，可以指定資料指標類型。 它會使用 SQL_ATTR_CURSOR_TYPE 陳述式屬性。 如果應用程式未明確指定類型，就會使用順向資料指標。 若要取得混合式資料指標，指定索引鍵集驅動資料指標的應用程式，但宣告索引鍵集大小小於結果集大小。  
  
 索引鍵集驅動和混合的資料指標，應用程式也可以指定索引鍵集大小。 它會使用 SQL_ATTR_KEYSET_SIZE 陳述式屬性。 如果索引鍵集大小設定為 0，這是預設值，索引鍵集大小設定為結果集大小，且索引鍵集驅動資料指標。 開啟資料指標之後，就可以變更索引鍵集大小。  
  
 應用程式也可以設定資料列集大小;如需詳細資訊，請參閱 <<c0> [ 使用區塊資料指標](../../../odbc/reference/develop-app/using-block-cursors.md)稍早的這一節。
