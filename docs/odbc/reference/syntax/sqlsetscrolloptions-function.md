---
title: SQLSetScroll選項函數 |微軟文件
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetScrollOptions
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLSetScrollOptions
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC]
ms.assetid: 2a825ba7-7942-4c23-bcdb-c80dc12f8c86
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 056fc203581e1d5d8323b09ac62d692093d8c0f5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287262"
---
# <a name="sqlsetscrolloptions-function"></a>SQLSetScrollOptions 函式
**一致性**  
 版本介紹: ODBC 1.0 標準合規性: 已棄用  
  
 **摘要**  
 在 ODBC *3.x*中,ODBC 2.0 函數**SQLSetScrollOptions**已被對**SQLGetInfo**和**SQLSetStmtAttr**的呼叫所取代。  
  
> [!NOTE]
>  有關驅動程式管理員將此功能映射到 ODBC *2.x*應用程式使用 ODBC *3.x*驅動程式時的詳細資訊,請參閱附錄 G:向後相容性驅動程式指南中的[對應已棄用函數](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)。  
> 
> [!NOTE]
>  當驅動程式管理器對應**SQLSetScrollOption 的應用程式 SQLSetScrollOption**時,使用不支援**SQLSetScrollOption**的 ODBC *3.x*驅動程式時,驅動程式管理器將SQL_ROWSET_SIZE語句選項(而不是SQL_ATTR_ROW_ARRAY_SIZE語句屬性)設置為**SQLSetScrollOption**中的*RowsetSize*參數。 因此,當調用**SQLFetch**或**SQLFetchScroll**獲取多行時,應用程式無法使用**SQLSetScrollOptions。** 它只能在調用**SQLExtendedFetch**獲取多行時使用。  
  
## <a name="remarks"></a>備註  
 如果應用程式將在 64 位元作業系統上執行,請參閱[ODBC 64 位元資訊](../../../odbc/reference/odbc-64-bit-information.md)。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
