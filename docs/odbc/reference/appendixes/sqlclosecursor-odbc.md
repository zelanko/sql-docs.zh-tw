---
title: "SQLCloseCursor_ODBC |Microsoft 文件"
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
- SQLCloseCursor function [ODBC], ODBC
ms.assetid: 5e47e3f7-e1b8-451f-bf75-daa19b7c7271
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fcc680ec815afa700c00c9d8a69c5826944153a4
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlclosecursorodbc"></a>SQLCloseCursor_ODBC
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論使用**SQLCloseCursor**資料指標程式庫中的函式。 如需一般資訊**SQLCloseCursor**，請參閱[SQLCloseCursor 函數](../../../odbc/reference/syntax/sqlclosecursor-function.md)。  
  
 資料指標程式庫不支援呼叫**SQLCloseCursor**沒有開啟的資料指標。 嘗試進行這會傳回 SQLSTATE 24000 （無效的資料指標狀態）。 呼叫**SQLFreeStmt**與*選項*SQL_CLOSE 的任何資料指標開啟時支援資料指標程式庫。
