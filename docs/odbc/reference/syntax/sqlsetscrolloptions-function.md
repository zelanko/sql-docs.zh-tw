---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 77a85caefadb54c3db2716c4db18b504e02da996
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68342936"
---
# <a name="sqlsetscrolloptions-function"></a>SQLSetScrollOptions 函式
**標準**  
 引進的版本： ODBC 1.0 標準合規性：已淘汰  
  
 **摘要**  
 在 ODBC 3.x*中，odbc*2.0 函數**SQLSetScrollOptions**已由**SQLGetInfo**和**SQLSetStmtAttr**的呼叫所取代。  
  
> [!NOTE]
>  如需 ODBC 2.x 應用程式*使用 odbc 3.x* *驅動程式時*，驅動程式管理員將此函式對應至哪個功能的詳細資訊，請參閱附錄 G：驅動程式方針中的對應已被[取代](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)的函式，以取得回溯相容性。  
> 
> [!NOTE]
>  當驅動程式管理員對應的應用程式使用不支援**SQLSetScrollOptions**的*ODBC 3.X 驅動程式* **SQLSetScrollOptions**時，驅動程式管理員會將 SQL_ROWSET_SIZE 語句選項（而非 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性）設定為**SQLSetScrollOption**中的*RowsetSize*引數。 因此，在透過呼叫**SQLFetch**或**SQLFetchScroll**來提取多個資料列時，應用程式無法使用**SQLSetScrollOptions** 。 只有在透過呼叫**SQLExtendedFetch**來提取多個資料列時，才能使用此方法。  
  
## <a name="remarks"></a>備註  
 如果您的應用程式將在64位的作業系統上執行，請參閱[ODBC 64 位資訊](../../../odbc/reference/odbc-64-bit-information.md)。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
