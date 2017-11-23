---
title: "字串限制 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: ec1da65f-c69d-415d-bf75-8fda8aa2b39f
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 260a530210b2e336067f2036f632cf347c1654f9
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="string-limitations"></a>字串限制
SQL 陳述式字串的長度上限為 65000 個字元。  
  
 使用 Microsoft Access 驅動程式時，只有 SQL 92 字串常數 （使用單引號，不雙引號） 支援。  
  
 縱線字元 (&#124;) 不能在字串中，是否或不以回復括住的字元。  
  
 最大的互通性，應用程式應該傳遞字串參數，而不是傳遞加上引號的字串。
