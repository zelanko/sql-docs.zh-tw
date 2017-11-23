---
title: "目錄函數 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- catalog functions [ODBC], about catalog functions
- data dictionary [ODBC]
- catalog functions [ODBC]
- functions [ODBC], catalog functions
ms.assetid: 81ba9453-c085-47c0-b411-90ca6a5ee428
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: beb83e909364bba3a06cfbc17926447364db8ae1
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="catalog-functions"></a>目錄函數
所有資料庫都有概要說明如何將資料儲存在資料庫中的結構。 例如，簡單的銷售訂單資料庫可能顯示在下圖中，在其識別碼資料行用來連結資料表的結構。  
  
 ![顯示簡單的資料庫結構](../../../odbc/reference/develop-app/media/pr19.gif "pr19")  
  
 此結構，以及其他資訊的權限，例如儲存在稱為 「 資料庫的系統資料表的一組*類別目錄，*也稱為*資料字典*。  
  
 應用程式可以探索此結構，透過呼叫*目錄函數*。 目錄函式會傳回結果集，而且是中的資訊通常是透過實作**選取**陳述式在目錄中的資料表。 例如，應用程式可能要求的結果集包含系統上所有資料表，或是特定資料表中所有資料行的相關資訊。  
  
 此章節包含下列主題。  
  
-   [使用目錄資料](../../../odbc/reference/develop-app/uses-of-catalog-data.md)  
  
-   [ODBC 中的目錄函式](../../../odbc/reference/develop-app/catalog-functions-in-odbc.md)
