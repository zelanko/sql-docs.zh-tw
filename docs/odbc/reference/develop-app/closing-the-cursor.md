---
title: 關閉游標 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], closing
- closing cursors [ODBC]
ms.assetid: 4f19bf5e-6d8c-40ae-a975-cfd62a0790ec
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 723e40e6d83eed84ed93ee1eeab3535622ad5f04
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299138"
---
# <a name="closing-the-cursor"></a>關閉資料指標
當應用程式使用遊標完成時,它將調用**SQLCloseCursor**來關閉游標。 例如：  
  
```  
SQLCloseCursor(hstmt);  
```  
  
 在應用程式關閉游標之前,打開游標的語句不能用於大多數其他操作,例如執行另一個 SQL 語句。 有關開啟游標時可以呼叫的函數的完整清單,請參閱[附錄 B:ODBC 狀態轉換表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
> [!NOTE]  
>  要關閉游標,應用程式應呼叫**SQLCloseCursor**,而不是**SQLCancel**。  
  
 游標保持打開狀態,直到顯式關閉,除非提交或回滾事務,在這種情況下,某些數據源將關閉游標。 特別是,當**SQLFetch**返回SQL_NO_DATA時,到達結果集的末尾不會關閉游標。 即使空結果集上的游標(在語句成功執行但未返回任何行時創建的結果集)也必須顯式關閉。
