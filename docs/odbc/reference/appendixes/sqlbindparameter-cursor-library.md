---
title: SQLBindParameter （資料指標程式庫） |Microsoft 文件
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
- SQLBindParameter function [ODBC], Cursor Library
ms.assetid: 04c53e4c-cd1d-40b2-9997-684ebe43499f
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 54ee24f29d425bd24788d005fa8ad8a09d781a28
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sqlbindparameter-cursor-library"></a>SQLBindParameter （資料指標程式庫）
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論使用**SQLBindParameter**資料指標程式庫中的函式。 如需一般資訊**SQLBindParameter**，請參閱[SQLBindParameter 函數](../../../odbc/reference/syntax/sqlbindparameter-function.md)。  
  
 應用程式可以呼叫**SQLBindParameter**重新繫結參數，只要 C 資料類型、 資料行大小和小數位數的繫結的資料行維持不變。  
  
 資料指標程式庫支援的設定，若要使用繫結位移 SQL_ATTR_ROW_BIND_OFFSET_PTR 陳述式屬性。 (**SQLBindParameter**並沒有發生重新繫結呼叫。)  
  
 資料指標程式庫支援繫結資料在執行中參數。
