---
description: 目錄函式
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b75e6a40252f06f6b9e2105bd557fd35ded9243f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465940"
---
# <a name="catalog-functions"></a>目錄函式
所有資料庫都有一種結構，可概述如何將資料儲存在資料庫中。 例如，簡單的銷售訂單資料庫可能會有如下圖所示的結構，其中的識別碼資料行用來連結資料表。  
  
 ![顯示簡單資料庫的結構](../../../odbc/reference/develop-app/media/pr19.gif "pr19")  
  
 此結構以及其他資訊（例如許可權）都會儲存在稱為資料庫目錄的一組系統資料表中 *，* 也稱為 *資料字典*。  
  
 應用程式可以透過呼叫 *目錄*函式來探索此結構。 目錄函數會傳回結果集中的資訊，而且通常會透過 **SELECT** 語句針對目錄中的資料表來執行。 例如，應用程式可能要求的結果集包含系統上所有資料表，或是特定資料表中所有資料行的相關資訊。  
  
 此章節包含下列主題。  
  
-   [使用目錄資料](../../../odbc/reference/develop-app/uses-of-catalog-data.md)  
  
-   [ODBC 中的目錄函式](../../../odbc/reference/develop-app/catalog-functions-in-odbc.md)
