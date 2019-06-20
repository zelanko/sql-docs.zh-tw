---
title: SQL-92 相容性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], SQL-92 compliance
- desktop database drivers [ODBC], SQL-92 compliance
- SQL-92 compliance [ODBC]
- ODBC desktop database drivers [ODBC], SQL-92 compliance
ms.assetid: 50c8c7df-df01-4f4d-ad62-d059cf29d73a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cf6d8d056c1658a924de4b108d3c0d025e8a58f1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63313394"
---
# <a name="sql-92-compliance"></a>SQL-92 相容性
ODBC 桌面資料庫驅動程式和基礎的 Microsoft Jet 引擎並非 SQL-92 相容。 它們支援 SQL-92 中已定義的許多功能。 驅動程式支援某些功能不支援以 SQL-92。 如需詳細資訊，請參閱 < *Microsoft Jet Database Engine 程式設計人員指南*。 兩者之間的主要差異如下：  
  
-   桌面資料庫驅動程式所使用的 SQL 支援指定的 SQL-92 更強大的運算式。  
  
-   不同的規則適用於 BETWEEN 述詞。  
  
-   桌面資料庫驅動程式和 ANSI SQL 所使用的 SQL 支援不同的關鍵字。  
  
 Microsoft Jet SQL 不支援下列 SQL-92 功能：  
  
-   安全性陳述式，例如授與和鎖定。  
  
-   相異彙總函式參考。  
  
 下列功能是沒有指定 SQL-92 桌面資料庫驅動程式所使用的 SQL 中的增強功能：  
  
-   提供支援交叉資料表查詢的轉換陳述式。  
  
-   額外的彙總函式 (**StDev**並**VarP**)。  
  
> [!NOTE]  
>  桌面資料庫驅動程式支援標準的 ANSI 語法 %（百分比） 及 _ （底線），不 * （星號） 和嗎？ （問號）。
