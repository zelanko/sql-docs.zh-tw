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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68054117"
---
# <a name="limitations-of-using-keyset-driven-cursors"></a>使用索引鍵集驅動資料指標的限制
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 所提供的 ODBC 驅動程式。  
  
 您必須能夠抓取所查詢資料表的單一 ROWID 資料行。 索引鍵集驅動資料指標不能用於包含 DISTINCT、GROUP BY、UNION、INTERSECT 或減號子句的聯結、查詢或語句。  
  
 此外，如果您的應用程式使用資料表別名，索引鍵集驅動資料指標將無法使用;需要順向或靜態資料指標類型。 使用索引鍵集資料指標類型與資料表別名會導致下列錯誤： "[Microsoft] [ODBC driver for Oracle] 無法在聯結上使用索引鍵集驅動資料指標，搭配 union、intersect 或減號或 on 唯讀結果集。"  
  
> [!NOTE]  
>  由於驅動程式處理傳送至 Oracle 伺服器之 SQL 語句的方式，Oracle 內部會傳回下列錯誤訊息：「TNSNAMES.ORA-00964：資料表名稱不在清單中。」
