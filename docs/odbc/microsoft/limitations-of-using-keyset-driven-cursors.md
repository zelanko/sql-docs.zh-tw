---
title: 使用索引鍵集驅動資料指標的限制 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], cursors
- keyset-driven cursors [ODBC]
ms.assetid: 59d86fed-387c-4719-9550-36343e74da44
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0c35f900faf1a30788b3642af3fdd65d672951d5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68054117"
---
# <a name="limitations-of-using-keyset-driven-cursors"></a>使用索引鍵集驅動資料指標的限制
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用所提供的 ODBC 驅動程式。  
  
 您必須能夠擷取查詢之資料表的單一 ROWID 資料行。 聯結、 查詢或陳述式包含 DISTINCT、 GROUP BY、 UNION、 INTERSECT 或減去子句，則無法使用索引鍵集驅動資料指標。  
  
 此外，如果您的應用程式會使用資料表別名，索引鍵集驅動資料指標將無法運作;順向或靜態資料指標類型所需。 使用索引鍵集資料指標類型，以資料表別名會導致下列錯誤: 「 [Microsoft] [ODBC driver for Oracle] 無法使用索引鍵集驅動資料指標聯結與 union、 intersect 或減去或唯讀結果集。 」  
  
> [!NOTE]  
>  由於驅動程式會處理傳送到 Oracle 伺服器的 SQL 陳述式的方式，Oracle 在內部會傳回下列錯誤訊息：「 ORA 00964： 資料表名稱不在清單中。 」
