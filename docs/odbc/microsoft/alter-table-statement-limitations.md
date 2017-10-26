---
title: "ALTER 資料表陳述式的限制 |Microsoft 文件"
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
- ODBC SQL grammar, ALTER TABLE statement limitations
- ALTER TABLE statement limitations [ODBC]
ms.assetid: f3e88f85-edf4-47cd-a822-292b106ddb34
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6c50ea6550e9dfb255c87886e4e0375240bcd2ae
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="alter-table-statement-limitations"></a>ALTER 資料表陳述式的限制
DBASE 或 Paradox 驅動程式使用時，一旦在建立索引，並加入新的記錄，無法由 ALTER TABLE 陳述式變更資料表的結構，除非卸除索引和資料表的內容會被刪除。  
  
 ALTER TABLE 陳述式不支援的 Microsoft Excel 或文字驅動程式。  
  
> [!NOTE]  
>  當您使用 Paradox 驅動程式而不需要實作 Borland Database Engine 時，不支援 ALTER TABLE 陳述式。僅讀取和附加允許陳述式。

