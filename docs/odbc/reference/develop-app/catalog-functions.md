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
manager: craigg
ms.openlocfilehash: 268d5f00d787cef8dfdcb29bd9e091f81a5ed2c9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63125577"
---
# <a name="catalog-functions"></a>目錄函式
所有的資料庫有概述如何將資料儲存在資料庫中的結構。 例如，簡單的銷售訂單的資料庫可能顯示在下圖中，在其識別碼資料行用來連結資料表的結構。  
  
 ![顯示簡單資料庫的結構](../../../odbc/reference/develop-app/media/pr19.gif "pr19")  
  
 此結構，以及其他資訊，例如權限，會儲存在稱為 「 資料庫的系統資料表的一組*目錄中，* 也稱為*資料字典*。  
  
 應用程式可以探索這個結構，透過呼叫*目錄函式*。 目錄函式會傳回中結果集的資訊通常是透過實作**選取**陳述式依據類別目錄中的資料表。 例如，應用程式可能要求的結果集包含系統上所有資料表，或是特定資料表中所有資料行的相關資訊。  
  
 此章節包含下列主題。  
  
-   [使用目錄資料](../../../odbc/reference/develop-app/uses-of-catalog-data.md)  
  
-   [ODBC 中的目錄函式](../../../odbc/reference/develop-app/catalog-functions-in-odbc.md)
