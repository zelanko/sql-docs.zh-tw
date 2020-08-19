---
description: 使用索引鍵集驅動資料指標的限制
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 611bc032c51760742e5dce4dfbd8e1fa4fe33d0f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483471"
---
# <a name="limitations-of-using-keyset-driven-cursors"></a>使用索引鍵集驅動資料指標的限制
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 提供的 ODBC 驅動程式。  
  
 您必須能夠為所查詢的資料表取出單一 ROWID 資料行。 索引鍵集驅動的資料指標無法用於包含 DISTINCT、GROUP BY、UNION、INTERSECT 或減號子句的聯結、查詢或語句。  
  
 此外，如果您的應用程式使用資料表別名，索引鍵集驅動的資料指標將無法運作;需要順向或靜態資料指標類型。 使用具有資料表別名的索引鍵集資料指標類型，會導致下列錯誤： "[Microsoft] [ODBC driver for Oracle] 無法在 join 上使用索引鍵集驅動資料指標，其 union、intersect 或減號或 on read only 結果集。"  
  
> [!NOTE]  
>  因為驅動程式處理傳送至 Oracle 伺服器之 SQL 語句的方式，所以 Oracle 會在內部傳回下列錯誤訊息：「TNSNAMES.ORA-00964：不在清單中的資料表名稱」。
