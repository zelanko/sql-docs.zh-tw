---
title: 參數值檢查 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6c6e4de16c4a1a80be893acbc7a1993b375f2fee
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298818"
---
# <a name="argument-value-checks"></a>引數值檢查
驅動程式管理員檢查以下類型的參數。 除非另有說明,否則驅動程式管理器將返回SQL_ERROR參數值中的錯誤。  
  
-   環境、連接和語句句柄通常不能為空指標。 驅動程式管理器在找到空句柄時返回SQL_INVALID_HANDLE。  
  
-   所需的指標參數(如**SQLAllocHandle**中的*Output HandlePtr*和**SQLSetCursorName**中的*CursorName)* 不能為空指標。  
  
-   不支援特定於驅動程式的值的選項標誌必須是一個法定值。 例如 **,SQLSetPos**中的*操作*必須SQL_POSITION、SQL_REFRESH、SQL_UPDATE、SQL_DELETE或SQL_ADD。  
  
-   驅動程式支援的 ODBC 版本中必須支援選項標誌。 例如,在調用 ODBC 2.0 驅動程式時,無法SQL_ASYNC_MODE **SQLGetInfo**中的*資訊類型*(在 ODBC 3.0 中引入)。  
  
-   列和參數編號必須大於 0 或大於或等於 0,具體取決於函數。 驅動程式必須基於當前結果集或 SQL 語句檢查這些參數值的上限。  
  
-   長度/指示器參數和數據緩衝區長度參數必須包含適當的值。 例如,在**SQLColumns** *(NameLength3)* 中指定表名長度的參數必須SQL_NTS或大於 0 的值;**SQLDescribeCol**中的*緩衝區長度*必須大於或等於 0。 驅動程式可能還需要檢查這些參數。 例如,它可能會檢查*NameLength3*小於或等於資料源中表名的最大長度。
