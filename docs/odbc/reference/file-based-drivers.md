---
description: 以檔案為基礎的驅動程式
title: 以檔案為基礎的驅動程式 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 770e8560c540e8423aebf0a79c0e8ee5c124c8e3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429080"
---
# <a name="file-based-drivers"></a>以檔案為基礎的驅動程式
以檔案為基礎的驅動程式會與資料來源搭配使用，例如不提供驅動程式要使用之獨立資料庫引擎的 dBASE。 這些驅動程式會直接存取實體資料，而且必須執行資料庫引擎來處理 SQL 語句。 作為標準做法，以檔案為基礎之驅動程式中的資料庫引擎會執行最小 SQL 一致性層級所定義的 ODBC SQL 子集;如需此一致性層級中的 SQL 語句清單，請參閱 [附錄 C： SQL 文法](../../odbc/reference/appendixes/appendix-c-sql-grammar.md)。  
  
 相較于以檔案為基礎的驅動程式與 DBMS 為基礎的驅動程式，以檔案為基礎的驅動程式較難寫入，因為資料庫引擎元件的設定較不復雜，因為沒有網路片段，且較不強大，因為很多人有時間撰寫資料庫引擎，其功能與資料庫公司所產生的強大。  
  
 下圖顯示以檔案為基礎之驅動程式的兩個不同設定，其中一個資料位於本機，而另一個則位於網路檔案伺服器上。  
  
 ![以檔案為基礎之驅動程式的兩個設定&#45;](../../odbc/reference/media/pr06.gif "pr06")
