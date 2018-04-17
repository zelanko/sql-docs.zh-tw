---
title: Sql-92 相容性 |Microsoft 文件
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
- Jet-based ODBC drivers [ODBC], SQL-92 compliance
- desktop database drivers [ODBC], SQL-92 compliance
- SQL-92 compliance [ODBC]
- ODBC desktop database drivers [ODBC], SQL-92 compliance
ms.assetid: 50c8c7df-df01-4f4d-ad62-d059cf29d73a
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 09b1a044a362207b5bc1c04d3a90e210ad7c8137
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sql-92-compliance"></a>Sql-92 相容性
ODBC 桌面資料庫驅動程式和基礎 Microsoft Jet 引擎不是以 sql-92 相容。 它們支援以 sql-92 定義的許多功能。 驅動程式中支援某些功能不支援以 sql-92。 如需詳細資訊，請參閱*Microsoft Jet 資料庫引擎程式設計人員指南*。 兩者之間的主要差異如下：  
  
-   桌面資料庫驅動程式所使用的 SQL 支援比指定的 SQL 92 功能更強大的運算式。  
  
-   不同的規則適用於 BETWEEN 述詞。  
  
-   ANSI SQL 和桌面資料庫驅動程式所使用的 SQL 支援不同的關鍵字。  
  
 Microsoft Jet SQL 不支援下列 SQL 92 功能：  
  
-   安全性陳述式，例如授與和鎖定。  
  
-   相異彙總函式的參考。  
  
 下列功能是未指定的 SQL 92 桌面資料庫驅動程式所使用的 SQL 中的增強功能：  
  
-   提供支援交叉資料表查詢轉換的陳述式。  
  
-   其他彙總函式 (**StDev**和**VarP**)。  
  
> [!NOTE]  
>  桌面資料庫驅動程式支援標準的 ANSI 語法 （百分比） %和 _ （底線），不 * （星號） 和嗎？ （問號）。
