---
title: 參數繫結偏移量 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- offsets of parameters [ODBC]
- binding offsets of parameters [ODBC]
ms.assetid: 309339e9-9ccd-4a58-8aa4-b6dc88f4eb7c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: de67b230883f3cf8a582e73ce82e8c4bd7d21ad0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282485"
---
# <a name="parameter-binding-offsets"></a>參數繫結位移
應用程式可以指定在調用**SQLExecDirect**或**SQLExecute**時將偏移量添加到綁定參數緩衝區位址和相應的長度/指示器緩衝區位址。 這些添加的結果確定這些操作中使用的位址。  
  
 繫結位移允許應用程式變更繫結,而無需為以前綁定的參數呼叫**SQLBind 參數**。 呼叫**SQLBind 參數**以重新繫結參數會更改緩衝區位址和長度/指示器指標。 另一方面,使用偏移重新綁定只需向現有綁定參數緩衝區位址和長度/指示器緩衝區位址添加偏移。 使用偏移時,綁定是應用程式緩衝區佈局方式的"範本",應用程式可以通過更改偏移量將此"範本"移動到不同的記憶體區域。 可以隨時指定新的偏移量,並且始終添加到最初綁定的值。  
  
 要指定綁定偏移量,應用程式將SQL_ATTR_PARAM_BIND_OFFSET_PTR語句屬性設置到 SQLINTEGER 緩衝區的位址。 在應用程式呼叫使用綁定的函數之前,只要參數緩衝區位址和長度/指示器緩衝區位址都不是 0,並且綁定參數在 SQL 語句中,它將在此緩衝區中放置一個偏移以位元組為單位。 位址和偏移量的總和必須為有效位址。 (這意味著偏移量和添加到偏移的位址都無效,只要其總和是有效的位址。  
  
> [!NOTE]  
>  ODBC 2 不支援綁定偏移。*x*驅動程式。
