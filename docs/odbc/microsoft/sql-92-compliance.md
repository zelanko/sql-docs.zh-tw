---
title: SQL-92 合規性 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300698"
---
# <a name="sql-92-compliance"></a>SQL-92 相容性
ODBC 桌面資料庫驅動程式和基礎的 Microsoft Jet 引擎不符合 SQL-92。 它們支援 SQL-92 中定義的許多功能。 SQL-92 不支援驅動程式中支援的某些功能。 有關詳細資訊,請參閱 Microsoft*噴氣資料庫引擎程式師指南*。 以下是兩者之間的主要區別:  
  
-   桌面資料庫驅動程式使用的 SQL 支援比 SQL-92 指定的運算式更強大的運算式。  
  
-   不同的規則適用於"之間"謂詞。  
  
-   桌面資料庫驅動程式和 ANSI SQL 使用的 SQL 支援不同的關鍵字。  
  
 微軟 Jet SQL 不支援以下 SQL-92 功能:  
  
-   安全語句,如 GRANT 和 LOCK。  
  
-   帶聚合函式引用的  
  
 以下功能是 SQL-92 未指定的桌面資料庫驅動程式使用的 SQL 中的增強功能:  
  
-   提供對交叉表查詢支援的 TRANSFORM 語句。  
  
-   其他聚合函數(**StDev**和**VarP**)。  
  
> [!NOTE]  
>  桌面資料庫驅動程式支援百分比(百分比)和 # (下劃線)、而不是 * (星號)和 (問號)。
