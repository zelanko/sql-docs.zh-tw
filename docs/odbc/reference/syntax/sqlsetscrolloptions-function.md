---
title: SQLSetScrollOptions 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetScrollOptions
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetScrollOptions
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC]
ms.assetid: 2a825ba7-7942-4c23-bcdb-c80dc12f8c86
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dbdd2038bc217a7ca2a2efe08940c03c5da5d8f0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62985244"
---
# <a name="sqlsetscrolloptions-function"></a>SQLSetScrollOptions 函式
**合規性**  
 導入的版本：ODBC 1.0 標準的合規性：已被取代  
  
 **摘要**  
 在 ODBC 3 *.x*，ODBC 2.0 函式**SQLSetScrollOptions**已取代呼叫**SQLGetInfo**並**SQLSetStmtAttr**。  
  
> [!NOTE]
>  如需有關什麼驅動程式管理員會對應到此函式時 ODBC 2 *.x*應用程式使用 ODBC 3 *.x*驅動程式，請參閱[對應已被取代的函式](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)附錄 g:為了與舊版相容的驅動程式指導方針。  
> 
> [!NOTE]
>  當驅動程式管理員會將對應**SQLSetScrollOptions**應用程式使用 ODBC 3 *.x*不支援的驅動程式**SQLSetScrollOptions**，驅動程式管理員設定 SQL_ROWSET_SIZE 陳述式選項，而不是 SQL_ATTR_ROW_ARRAY_SIZE 陳述式屬性， *RowsetSize*中的引數**SQLSetScrollOption**。 如此一來， **SQLSetScrollOptions**呼叫擷取多個資料列時無法由應用程式**SQLFetch**或是**SQLFetchScroll**。 它可以用於擷取多個資料列呼叫時，才**SQLExtendedFetch**。  
  
## <a name="remarks"></a>備註  
 如果您的應用程式將在 64 位元作業系統上執行，請參閱[ODBC 64 位元資訊](../../../odbc/reference/odbc-64-bit-information.md)。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
