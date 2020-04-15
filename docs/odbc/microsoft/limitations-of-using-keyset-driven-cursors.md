---
title: 使用鍵集驅動游標的限制 |微軟文件
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
ms.openlocfilehash: 2aeb5a0c50192118dfff8ed7d866c3911c2b4007
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284148"
---
# <a name="limitations-of-using-keyset-driven-cursors"></a>使用索引鍵集驅動資料指標的限制
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 而是使用 Oracle 提供的 ODBC 驅動程式。  
  
 您必須能夠檢索查詢的表的單個 ROWID 列。 鍵集驅動的游標不能用於包含"差異"、組 BY、UNION、INTERSECT 或 MINUS 子句的聯接、查詢或語句。  
  
 此外,如果應用程式使用表別名,則鍵集驅動的游標將不起作用;如果應用程式使用表別名,則鍵集驅動的游標將不起作用。需要僅轉發或靜態游標類型。 使用帶有表別名的鍵集游標類型將導致以下錯誤:"[Microsoft][Oracle 的 ODBC 驅動程式]無法在聯接、聯合、相交或減或只讀結果集上使用 Keyset 驅動的游標。  
  
> [!NOTE]  
>  由於驅動程式處理發送到 Oracle 伺服器的 SQL 語句的方式,Oracle 內部返回以下錯誤消息:「ORA-00964:表名不在 FROM 列表中。
