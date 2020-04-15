---
title: 預設 C 資料型態 :微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], pseudo-type identifiers
- pseudo-type identifiers [ODBC], about pseudo-type identifiers
- pseudo-type identifiers [ODBC]
ms.assetid: 229140ae-af8f-4ec8-9ccf-1e92360e0bac
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fdb787580e1c79df805f468416ab8993a1d32a26
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307049"
---
# <a name="default-c-data-types"></a>預設 C 資料類型
如果應用程式在**SQLBindCol、SQLGetData**或**SQLBind 參數**中指定SQL_C_DEFAULT ,則驅動程式假定輸出或輸入緩衝區的 C 資料類型對應於緩衝區綁定到的列或**SQLGetData**參數的 SQL 數據類型。  
  
> [!IMPORTANT]  
>  可互操作的應用程式不應使用SQL_C_DEFAULT。 相反,它們應始終指定他們正在使用的緩衝區的 C 類型。 這是因為驅動程式無法始終正確確定預設 C 類型,原因如下:  
  
-   如果 DBMS 升級列或參數的 SQL 資料類型,則驅動程式無法確定列或參數的原始 SQL 資料類型。 因此,它無法確定相應的預設 C 數據類型。  
  
-   如果驅動程式無法確定是否對特定列或參數進行簽名(DBMS 處理時通常的情況)驅動程式無法確定應簽名還是未簽名相應的預設 C 資料類型。  
  
     由於SQL_C_DEFAULT僅為程式設計方便而提供,因此當應用程式指定實際C資料類型時,不會丟失任何功能。  
  
 在本附錄的後面部分,顯示每個 SQL 資料類型的預設 C 資料類型的表包含在[將數據從 SQL 轉換為 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)中。
