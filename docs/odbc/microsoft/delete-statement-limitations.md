---
title: DELETE 陳述式的限制 |Microsoft 文件
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
- DELETE statement limitations [ODBC]
- ODBC SQL grammar, DELETE statement limitations
ms.assetid: 084761fe-e65b-4f38-ba4f-69884b2a7700
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 45386d8278e968b55fba5881dfe9b914bc23f454
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="delete-statement-limitations"></a>刪除陳述式的限制
DELETE 陳述式不支援 Microsoft Excel 或文字驅動程式。 請注意，文字驅動程式支援 INSERT 陳述式。  
  
 DBASE 驅動程式不支援壓縮資料表來移除 「 刪除 」 的值。  
  
 Paradox 驅動程式從資料表刪除資料列時，該資料表必須有唯一的索引 （Paradox 主索引鍵）。
