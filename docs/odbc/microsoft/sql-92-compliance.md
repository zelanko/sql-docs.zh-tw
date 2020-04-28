---
title: SQL-92 合規性 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9ac0ae5873e545afb8fcac9dd003c984b1ed303a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300698"
---
# <a name="sql-92-compliance"></a>SQL-92 相容性
ODBC 桌面資料庫驅動程式和基礎 Microsoft Jet 引擎不符合 SQL-92 規範。 它們支援 SQL-92 中已定義的許多功能。 SQL-92 不支援驅動程式中支援的某些功能。 如需詳細資訊，請參閱《 *Microsoft Jet 資料庫引擎程式設計人員指南》*。 以下是兩者之間的主要差異：  
  
-   桌面資料庫驅動程式所使用的 SQL 支援比 SQL-92 所指定更強大的運算式。  
  
-   不同的規則適用于 BETWEEN 述詞。  
  
-   桌面資料庫驅動程式和 ANSI SQL 所使用的 SQL 支援不同的關鍵字。  
  
 Microsoft Jet SQL 不支援下列 SQL-92 功能：  
  
-   安全性語句，例如 GRANT 和 LOCK。  
  
-   與彙總函式參考相異。  
  
 下列功能是桌面資料庫驅動程式（不是由 SQL-92 指定）所使用的 SQL 增強功能：  
  
-   提供交叉分析查詢支援的 TRANSFORM 語句。  
  
-   其他彙總函式（**StDev**和**VarP**）。  
  
> [!NOTE]  
>  桌面資料庫驅動程式支援% （percent）和 _ （底線）的標準 ANSI 語法，而非 * （星號）和？ (問號)。
