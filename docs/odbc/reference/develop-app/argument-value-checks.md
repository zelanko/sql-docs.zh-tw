---
title: 引數值檢查 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- argument value checks [ODBC]
- driver manager [ODBC], error checking
ms.assetid: 37a65f8b-83aa-456c-b7cf-500404abb38a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 013c8f80a672ed691e7519b318206c406171cfbc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68077110"
---
# <a name="argument-value-checks"></a>引數值檢查
驅動程式管理員會檢查下列類型的引數。 除非另有注明，否則驅動程式管理員會針對引數值中的錯誤傳回 SQL_ERROR。  
  
-   環境、連接和語句控制碼通常不可以是 null 指標。 驅動程式管理員在找到 null 控制碼時，會傳回 SQL_INVALID_HANDLE。  
  
-   必要的指標引數（例如**SQLAllocHandle**中的*OutputHandlePtr*和**SQLSetCursorName**中的*CursorName* ）不可以是 null 指標。  
  
-   不支援驅動程式特定值的選項旗標必須是合法的值。 例如， **SQLSetPos**中的*Operation*必須是 SQL_POSITION、SQL_REFRESH、SQL_UPDATE、SQL_DELETE 或 SQL_ADD。  
  
-   驅動程式支援的 ODBC 版本中必須支援選項旗標。 例如，呼叫 ODBC 2.0 驅動程式時，無法 SQL_ASYNC_MODE **SQLGetInfo**中的*INFOTYPE* （在 ODBC 3.0 中引進）。  
  
-   視函式而定，資料行和參數編號必須大於0或大於或等於0。 驅動程式必須根據目前的結果集或 SQL 語句來檢查這些引數值的上限。  
  
-   長度/指標引數和資料緩衝區長度引數必須包含適當的值。 例如，指定**SQLColumns** （*NameLength3*）中資料表名稱長度的引數必須 SQL_NTS 或大於0的值;**SQLDescribeCol**中的*BufferLength*必須大於或等於0。 驅動程式可能也需要檢查這些引數。 例如，它可能會檢查*NameLength3*是否小於或等於資料來源中資料表名稱的最大長度。
