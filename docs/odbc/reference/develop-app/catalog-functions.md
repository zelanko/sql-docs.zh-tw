---
title: 目錄函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], about catalog functions
- data dictionary [ODBC]
- catalog functions [ODBC]
- functions [ODBC], catalog functions
ms.assetid: 81ba9453-c085-47c0-b411-90ca6a5ee428
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 232d2e9b7e9eb695a40058075ea511392e464a32
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68064406"
---
# <a name="catalog-functions"></a>目錄函式
所有資料庫都有一個結構，說明如何將資料儲存在資料庫中。 例如，簡單的銷售訂單資料庫可能具有下圖所示的結構，其中識別碼資料行是用來連結資料表。  
  
 ![顯示簡單資料庫的結構](../../../odbc/reference/develop-app/media/pr19.gif "pr19")  
  
 這個結構連同其他資訊（例如許可權）會儲存在稱為資料庫目錄的一組系統資料表中 *，* 這也稱為*資料字典*。  
  
 應用程式可以透過呼叫*目錄函數*來探索此結構。 目錄函數會傳回結果集中的資訊，而且通常會透過目錄中資料表的**SELECT**語句來執行。 例如，應用程式可能要求的結果集包含系統上所有資料表，或是特定資料表中所有資料行的相關資訊。  
  
 此章節包含下列主題。  
  
-   [使用目錄資料](../../../odbc/reference/develop-app/uses-of-catalog-data.md)  
  
-   [ODBC 中的目錄函式](../../../odbc/reference/develop-app/catalog-functions-in-odbc.md)
