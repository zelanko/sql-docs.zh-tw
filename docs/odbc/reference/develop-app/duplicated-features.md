---
title: 重複的功能 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- duplicated functions [ODBC]
- compatibility [ODBC], duplicated functions
- ODBC drivers [ODBC], backward compatibility
- functions [ODBC], duplicated functions
- backward compatibility [ODBC], duplicated functions
ms.assetid: 641b16bc-f791-46d8-b093-31736473fe3d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 00f5529cfbfacebcad78a0a4433e84f34034694a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300478"
---
# <a name="duplicated-features"></a>重複的功能
以下 ODBC *2.x*函數已由 ODBC *3.x*函數複製。 因此,ODBC *2.x*函數在 ODBC *3.x*中被棄用。 ODBC *3.x*函數稱為替換函數。  
  
 當應用程式使用棄用的 ODBC *2.x*函數,而基礎驅動程式是 ODBC *3.x*驅動程式時,驅動程式管理器將函數調用映射到相應的替換函數。 這個規則的唯一例外是**SQL 延伸 。** (請參閱下表末尾的腳註。有關這些映射的詳細資訊,請參閱附錄 G:向後相容性的驅動程式指南中[映射已棄用函數](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)。  
  
 當應用程式使用替換函數,基礎驅動程式是 ODBC *2.x*驅動程式時,驅動程式管理器將函數調用映射到相應的棄用函數。  
  
|ODBC *2.x*功能|ODBC *3.x*功能|  
|-------------------------|-------------------------|  
|**SQLAlloc 連線**|**SQLAllocHandle**|  
|**SQLAllocEnv**|**SQLAllocHandle**|  
|**SQLAllocStmt**|**SQLAllocHandle**|  
|**SQLColattributes**|**SQLColAttribute**|  
|**SQLError**|**SQLGetDiagRec**|  
|**SQL 延伸到**%1】...|**SQLFetchScroll**|  
|**SQLFreeConnect**|**SQLFreeHandle**|  
|**SQLFreeEnv**|**SQLFreeHandle**|  
|**SQLGetConnectOption**|**SQLGetConnectAttr**|  
|**SQLGetStmtOption**|**SQLGetStmtAttr**|  
|**SQLParamOptions**|**SQLSetStmtAttr**, **SQLGetstmtAttr**|  
|**SQLSet 連線選項**|**SQLSetConnectAttr**|  
|**SQLSetParam**|**SQLBindParameter**|  
|**SQLSetStmtOption**|**SQLSetStmtAttr**|  
|**SQLTransact**|**SQLEndTran**|  
  
 [1] 函數**SQL 擴展獲取**是重複的功能;**SQLFetchScroll**在 ODBC *3.x*中提供了相同的功能。 但是,當與 ODBC *3.x*驅動程式發生對抗時,驅動程式管理器不會將**SQLAtoFetch**映射到**SQLFetchScroll。** 有關詳細資訊,請參閱[驅動程式管理器](../../../odbc/reference/appendixes/what-the-driver-manager-does.md)在附錄 G 中的「驅動程式管理器」中所做的「驅動程式指南」。 當與 ODBC *2.x*驅動程式發生對抗時,驅動程式管理員將**SQLFetchScroll**映射到**SQL 擴充 。**  
  
> [!NOTE]
>  函數**SQLBindParam**是一個特例。 **SQLBindParam**是重複的功能。 這不是 ODBC *2.x*函數,而是開放組和 ISO 標準中存在的函數。 此函數提供的功能完全由**SQLBind 參數**的功能包起來。 因此,當基礎驅動程式是 ODBC *3.x*驅動程式時,驅動程式管理器將對**SQLBindParam**的呼叫映射到**SQLBind 參數**。 但是,當基礎驅動程式是 ODBC *2.x*驅動程式時,驅動程式管理器不執行此映射。
