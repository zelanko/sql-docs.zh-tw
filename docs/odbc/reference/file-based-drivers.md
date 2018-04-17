---
title: 以檔案為基礎的驅動程式 |Microsoft 文件
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
- file-based drivers [ODBC]
- ODBC architecture [ODBC], drivers
- drivers [ODBC], file-based drivers
ms.assetid: d92e0c5c-d176-4282-bbe1-d449e2223d50
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e63c8026b31140f5ad1f94c99f143670d31c5c78
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="file-based-drivers"></a>以檔案為基礎的驅動程式
以檔案為基礎的驅動程式會搭配等 dBASE 不提供驅動程式使用的獨立資料庫引擎的資料來源。 這些驅動程式會直接存取實體的資料，而且必須實作資料庫引擎處理序的 SQL 陳述式。 標準作法是以檔案為基礎的驅動程式中的資料庫引擎會實作最小 SQL 一致性層級; 所定義的 ODBC SQL 子集如需此一致性層級中的 SQL 陳述式的清單，請參閱[附錄 c: SQL 文法](../../odbc/reference/appendixes/appendix-c-sql-grammar.md)。  
  
 在比較的檔案為基礎和 DBMS 架構驅動程式，以檔案為基礎的驅動程式不難撰寫的資料庫引擎元件，較不複雜，無法設定，因為沒有網路棋子，因為且較不強大因為少數的人員寫入資料庫的時間引擎功能一樣強大資料庫公司所產生。  
  
 下圖顯示兩個不同的組態，以檔案為基礎的驅動程式，一個資料位於本機，因為其所在的其他網路檔案伺服器上。  
  
 ![檔案的兩個組態&#45;基礎驅動程式](../../odbc/reference/media/pr06.gif "pr06")
