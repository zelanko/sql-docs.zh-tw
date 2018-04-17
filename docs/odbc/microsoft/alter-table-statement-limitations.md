---
title: ALTER 資料表陳述式的限制 |Microsoft 文件
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
ms.topic: article
helpviewer_keywords:
- ODBC SQL grammar, ALTER TABLE statement limitations
- ALTER TABLE statement limitations [ODBC]
ms.assetid: f3e88f85-edf4-47cd-a822-292b106ddb34
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 06af545611da90d51ad0fc82136a4cb1ecc3984c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="alter-table-statement-limitations"></a>ALTER 資料表陳述式的限制
DBASE 或 Paradox 驅動程式使用時，一旦在建立索引，並加入新的記錄，無法由 ALTER TABLE 陳述式變更資料表的結構，除非卸除索引和資料表的內容會被刪除。  
  
 ALTER TABLE 陳述式不支援的 Microsoft Excel 或文字驅動程式。  
  
> [!NOTE]  
>  當您使用 Paradox 驅動程式而不需要實作 Borland Database Engine 時，不支援 ALTER TABLE 陳述式。僅讀取和附加允許陳述式。
