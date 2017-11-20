---
title: "DELETE 陳述式的限制 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- DELETE statement limitations [ODBC]
- ODBC SQL grammar, DELETE statement limitations
ms.assetid: 084761fe-e65b-4f38-ba4f-69884b2a7700
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d8ffdb2fa548b03ee38c0f817675cb88ab4acf67
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="delete-statement-limitations"></a>刪除陳述式的限制
DELETE 陳述式不支援 Microsoft Excel 或文字驅動程式。 請注意，文字驅動程式支援 INSERT 陳述式。  
  
 DBASE 驅動程式不支援壓縮資料表來移除 「 刪除 」 的值。  
  
 Paradox 驅動程式從資料表刪除資料列時，該資料表必須有唯一的索引 （Paradox 主索引鍵）。

