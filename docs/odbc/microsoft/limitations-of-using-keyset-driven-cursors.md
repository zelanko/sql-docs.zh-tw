---
title: "使用索引鍵集驅動資料指標的限制 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], cursors
- keyset-driven cursors [ODBC]
ms.assetid: 59d86fed-387c-4719-9550-36343e74da44
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a6ecdac0639264140feb29cbe5023f81b407d231
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="limitations-of-using-keyset-driven-cursors"></a>使用索引鍵集驅動資料指標的限制
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用由 Oracle 提供的 ODBC 驅動程式。  
  
 您必須能夠擷取查詢之資料表的單一 ROWID 資料行。 索引鍵集驅動資料指標不能在聯結、 查詢或陳述式包含 DISTINCT、 GROUP BY、 UNION、 INTERSECT 或減號子句。  
  
 此外，如果您的應用程式會使用資料表別名，索引鍵集驅動資料指標將無法運作。需要的順向或靜態資料指標類型。 使用索引鍵集資料指標類型以資料表別名將會導致下列錯誤: 「 [Microsoft] [oracle 的 ODBC 驅動程式] 無法使用索引鍵集驅動資料指標上聯結與 union、 intersect 或減或唯讀結果集。 」  
  
> [!NOTE]  
>  驅動程式會處理傳送到 Oracle 伺服器的 SQL 陳述式的方式，因為 Oracle 內部傳回下列錯誤訊息: 「 ORA-TUT1-LESSON1-STEP2 00964： 資料表名稱不在清單中。 」
