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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077110"
---
# <a name="argument-value-checks"></a>引數值檢查
驅動程式管理員會檢查下列類型的引數。 除非另有註明，否則驅動程式管理員會傳回 SQL_ERROR 引數的值中的錯誤。  
  
-   環境、 連接和陳述式控制代碼通常不能是 null 指標。 驅動程式管理員會傳回 SQL_INVALID_HANDLE，當它找到空的控制代碼。  
  
-   需要指標引數，例如*OutputHandlePtr*中**SQLAllocHandle**並*Current*中**SQLSetCursorName**，不可為null 指標。  
  
-   不支援驅動程式專屬值的選項旗標必須是合法的值。 例如，*作業*中**SQLSetPos**必須 SQL_POSITION、 SQL_REFRESH、 SQL_UPDATE、 SQL_DELETE 或 SQL_ADD。  
  
-   選項旗標必須支援的驅動程式支援的 ODBC 版本。 例如，*資訊類型*中**SQLGetInfo**無法 SQL_ASYNC_MODE （在 ODBC 3.0 中引進） 時呼叫 ODBC 2.0 驅動程式。  
  
-   資料行和參數的數字必須大於 0 或大於或等於 0，視函數而定。 此驅動程式必須檢查這些根據目前的結果集或 SQL 陳述式的引數值的上限。  
  
-   長度/指標引數和資料緩衝區長度引數必須包含適當的值。 例如，指定中的資料表名稱的長度引數**SQLColumns** (*NameLength3*) 必須是 SQL_NTS 或值大於 0。*Columnsize*中**SQLDescribeCol**必須大於或等於 0。 驅動程式可能也需要檢查這些引數。 比方說，它可能會檢查*NameLength3*小於或等於資料來源中的資料表名稱的最大長度。
