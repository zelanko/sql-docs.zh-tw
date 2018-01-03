---
title: "引數的值檢查 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- argument value checks [ODBC]
- driver manager [ODBC], error checking
ms.assetid: 37a65f8b-83aa-456c-b7cf-500404abb38a
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2c5980573d67eff7b791af6f01d3881524312474
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="argument-value-checks"></a>引數的值檢查
驅動程式管理員會檢查下列類型的引數。 除非另有註明，否則驅動程式管理員會傳回 SQL_ERROR 引數的值中的錯誤。  
  
-   環境、 連接和陳述式控制代碼通常不能是 null 指標。 驅動程式管理員會傳回 SQL_INVALID_HANDLE，當它找到空的控制代碼。  
  
-   需要指標引數，例如*OutputHandlePtr*中**SQLAllocHandle**和*Current*中**SQLSetCursorName**，不可為null 指標。  
  
-   不支援驅動程式專屬值的選項旗標必須是合法的值。 例如，*作業*中**SQLSetPos**必須 SQL_POSITION、 SQL_REFRESH、 SQL_UPDATE、 SQL_DELETE 或 SQL_ADD。  
  
-   選項旗標必須支援的驅動程式支援的 ODBC 版本。 例如，*資訊類型*中**SQLGetInfo**不可 SQL_ASYNC_MODE （ODBC 3.0 中引進） 呼叫 ODBC 2.0 驅動程式時。  
  
-   資料行和參數的數字必須大於 0 或大於或等於 0，視函數而定。 驅動程式必須檢查這些根據目前結果集或 SQL 陳述式的引數值的數目上限。  
  
-   長度/指標引數和資料緩衝區的長度引數必須包含適當的值。 例如，指定中的資料表名稱的長度的引數**SQLColumns** (*NameLength3*) 必須是 SQL_NTS 或是值大於 0;*Columnsize*中**SQLDescribeCol**必須大於或等於 0。 驅動程式可能也需要檢查這些引數。 例如，它可能會檢查*NameLength3*小於或等於資料來源中的資料表名稱的最大長度。
