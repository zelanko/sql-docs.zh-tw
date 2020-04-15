---
title: 呼叫級介面 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], CLI
- CLI [ODBC], using CLI
- sending SQL statements to DBMS [ODBC]
- SQL [ODBC], CLI
- call-level interface [ODBC], using call-level interface
ms.assetid: 42257bb6-0bf1-4533-a4ef-4a6dd2aecb18
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4288a278f745d533c92d3d45892753ef1a74c2b3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306539"
---
# <a name="call-level-interfaces"></a>呼叫層級介面
將 SQL 語句發送到 DBMS 的最後一種技術是透過調用級介面 (CLI)。 調用級介面提供可由應用程式呼叫的 DBMS 函數庫。 因此,調用級介面不是試圖將 SQL 與其他程式設計語言混合,而是類似於大多數程式師習慣使用的常規庫,如 C 中的字串、I/O 或數學庫。 請注意,支援嵌入式 SQL 的 DBMS 已經具有調用級介面,該調用由預編譯器生成。 但是,這些呼叫沒有記錄,如有更改,恕不另行通知。  
  
 調用級介面通常用於用戶端/伺服器體系結構,其中應用程式(用戶端)駐留在一台電腦上,DBMS(伺服器)駐留在另一台電腦上。 應用程式在本地系統上調用 CLI 函數,這些調用透過網路發送到 DBMS 進行處理。  
  
 調用級介面類似於動態 SQL,因為 SQL 語句在運行時傳遞給 DBMS 進行處理,但它不同於整個嵌入式 SQL,因為沒有嵌入 SQL 語句,也不需要預編譯。  
  
 使用呼叫層介面通常涉及以下步驟:  
  
1.  應用程式呼叫 CLI 函數以連接到 DBMS。  
  
2.  應用程式生成 SQL 語句並將其放在緩衝區中。 然後,它調用一個或多個 CLI 函數將語句發送到 DBMS 以進行準備和執行。  
  
3.  如果語句是 SELECT 語句,則應用程式調用 CLI 函數以在應用程式緩衝區中返回結果。 通常,此函數一次返回一行或一列數據。  
  
4.  應用程式呼叫 CLI 函數以斷開與 DBMS 的連接。
