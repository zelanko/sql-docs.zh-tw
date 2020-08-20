---
description: SQLSetScrollOptions 函式
title: SQLSetScrollOptions 函式 |Microsoft Docs
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
ms.openlocfilehash: 0197c3756b76b480cd5370b5edff9d6fc88b201c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491205"
---
# <a name="sqlsetscrolloptions-function"></a>SQLSetScrollOptions 函式
**一致性**  
 引進的版本： ODBC 1.0 標準合規性：已淘汰  
  
 **總結**  
 在 ODBC 3.x *中，odbc*2.0 函式 **SQLSetScrollOptions** 已由呼叫 **SQLGetInfo** 和 **SQLSetStmtAttr**取代。  
  
> [!NOTE]
>  如需當 ODBC 2.x 應用程式*與 odbc 3.x* *驅動程式搭配*使用時，驅動程式管理員會將此函式對應至的詳細資訊，請參閱附錄 G：驅動程式指導方針中的[對應已淘汰](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)函式以提供回溯相容性。  
> 
> [!NOTE]
>  當驅動程式管理員針對使用不支援**SQLSetScrollOptions***之 ODBC 3.x 驅動程式的*應用程式對應**SQLSetScrollOptions**時，驅動程式管理員會將 SQL_ROWSET_SIZE 語句選項（而非 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性）設定為**SQLSetScrollOption**中的*RowsetSize*引數。 因此，應用程式在呼叫**SQLFetch**或**SQLFetchScroll**時，無法使用**SQLSetScrollOptions**來提取多個資料列。 只有在透過呼叫 **SQLExtendedFetch**來提取多個資料列時，才可以使用它。  
  
## <a name="remarks"></a>備註  
 如果您的應用程式將在64位的作業系統上執行，請參閱 [ODBC 64 位資訊](../../../odbc/reference/odbc-64-bit-information.md)。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
