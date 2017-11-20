---
title: "多個 hstmts （Paradox 驅動程式） |Microsoft 文件"
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
- multiple hstmts [ODBC]
- Paradox driver [ODBC], multiple hstmts
ms.assetid: 66aecd94-092d-43d4-9583-74f5e2990eac
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8720a5f196b9e7d2beddc2de2780ce5598c3dc35
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="multiple-hstmts-paradox-driver"></a>多個 hstmts （Paradox 驅動程式）
ODBC Paradox 驅動程式使用時，如果您想要使用一個以上*hstmt*資料表上執行查詢，資料表必須有唯一的索引 （Paradox 主索引鍵）。

