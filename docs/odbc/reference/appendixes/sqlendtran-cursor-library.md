---
title: "SQLEndTran （資料指標程式庫） |Microsoft 文件"
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
- SQLEndTran function [ODBC], Cursor Library
ms.assetid: 92340b87-9084-4838-a509-e9ca22d5fd5c
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 50b6c5ffec8dd088bdc730699cfa88abea860768
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlendtran-cursor-library"></a>SQLEndTran （資料指標程式庫）
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論使用**SQLEndTran**資料指標程式庫中的函式。 如需一般資訊**SQLEndTran**，請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。  
  
 資料指標程式庫不支援交易，並將傳遞至呼叫**SQLEndTran**直接到驅動程式。 不過，資料指標程式庫具有 SQL_CURSOR_ROLLBACK_BEHAVIOR 與 SQL_CURSOR_COMMIT_BEHAVIOR 資訊類型的資料來源所傳回支援的資料指標認可和回復行為：  
  
-   保留跨多筆交易的資料指標的資料來源，復原資料來源中的變更不會回復在資料指標程式庫的快取中。 若要讓比對資料來源中的資料的快取，應用程式必須關閉再重新開啟資料指標。  
  
-   關閉資料指標在交易界限的資料來源，資料指標程式庫會關閉資料指標，並刪除快取的連接上的所有陳述式。  
  
-   刪除已備妥的陳述式在交易界限的資料來源，應用程式必須 reprepare 上的連接，再重新加以所有備妥的陳述式。

