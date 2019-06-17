---
title: 檔案為基礎的驅動程式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- file-based drivers [ODBC]
- ODBC architecture [ODBC], drivers
- drivers [ODBC], file-based drivers
ms.assetid: d92e0c5c-d176-4282-bbe1-d449e2223d50
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 45d9203a08b9c70809e81fb3d9cf84a521017068
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62628595"
---
# <a name="file-based-drivers"></a>以檔案為基礎的驅動程式
使用 dBASE 等的資料來源未提供要使用的驅動程式的獨立資料庫引擎會使用檔案為基礎的驅動程式。 這些驅動程式會直接存取實體的資料，而且必須實作資料庫引擎處理序的 SQL 陳述式。 標準的方法是，檔案為基礎的驅動程式中的資料庫引擎會實作最小 SQL 一致性層級; 所定義的 ODBC SQL 子集如需此一致性層級中的 SQL 陳述式的清單，請參閱[附錄 c:SQL 文法](../../odbc/reference/appendixes/appendix-c-sql-grammar.md)。  
  
 在比較的檔案為基礎和以 DBMS 為基礎驅動程式，檔案為基礎的驅動程式是因為資料庫引擎元件，變得簡單許多設定，因為沒有任何網路項目，而撰寫的工作變得更難和權力較小因為幾位人員擁有寫入資料庫的時間產生資料庫公司一樣強大的引擎。  
  
 下圖顯示兩個不同的組態檔為基礎的驅動程式，其中的資料位於本機，另一個其所在的網路檔案伺服器上。  
  
 ![兩個組態檔的&#45;架構的驅動程式](../../odbc/reference/media/pr06.gif "pr06")
