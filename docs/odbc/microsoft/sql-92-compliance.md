---
description: SQL-92 相容性
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
ms.openlocfilehash: 7d978b236c45d442732cd3602c3fbbb6d16dfd8f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483431"
---
# <a name="sql-92-compliance"></a>SQL-92 相容性
ODBC Desktop 資料庫驅動程式和基礎 Microsoft Jet 引擎不符合 SQL-92 規範。 它們支援 SQL-92 中已定義的許多功能。 SQL-92 不支援驅動程式中支援的某些功能。 如需詳細資訊，請參閱《 *Microsoft Jet 資料庫引擎程式設計人員指南》*。 以下是兩者之間的主要差異：  
  
-   桌面資料庫驅動程式所使用的 SQL 支援比 SQL-92 所指定更強大的運算式。  
  
-   不同的規則適用于 BETWEEN 述詞。  
  
-   桌面資料庫驅動程式和 ANSI SQL 所使用的 SQL 支援不同的關鍵字。  
  
 下列 SQL-92 功能不受 Microsoft Jet SQL 支援：  
  
-   安全性語句，例如 GRANT 和 LOCK。  
  
-   與彙總函式參考相異。  
  
 下列功能是桌面資料庫驅動程式所使用 SQL 的增強功能，但這些功能並非由 SQL-92 指定：  
  
-   提供交叉資料表查詢支援的轉換語句。  
  
-    (**StDev** 和 **VarP**) 的其他彙總函式。  
  
> [!NOTE]  
>  桌面資料庫驅動程式支援% (%) 的標準 ANSI 語法，以及 _ (底線) ，而不是 * (星號) 和？ (問號)。
