---
title: 字串限制 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: ec1da65f-c69d-415d-bf75-8fda8aa2b39f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 61f81ff3da882095a0a6c41bb5061addd497a5d2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306059"
---
# <a name="string-limitations"></a>字串限制
SQL 語句字串的最大長度為 65,000 個字元。  
  
 使用 Microsoft Access 驅動程式時,僅支援 SQL-92 字串常量(帶有單引號,而不是雙引號)。  
  
 無論該字元是否包含在後引號中,都不能在字串中使用管道字元(&#124;)。  
  
 為了達到最大的互操作性,應用程式應傳遞參數中的字串,而不是傳遞引號字串。
