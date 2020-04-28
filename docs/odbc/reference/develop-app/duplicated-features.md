---
title: 重複的功能 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300478"
---
# <a name="duplicated-features"></a>重複的功能
ODBC *3.x 函數已重複下列 odbc 2.x*函*式。* 因此 *，odbc 2.x*函式在 odbc 3.x 中會被*取代。* *ODBC 3.x*函數稱為取代函式。  
  
 當應用程式使用已被取代*的 odbc 2.x*函式，而基礎驅動程式是 odbc 3.x*驅動程式*時，驅動程式管理員會將函式呼叫對應至相對應的取代函數。 此規則的唯一例外狀況是**SQLExtendedFetch**。 （請參閱下表結尾的註腳）。如需這些對應的詳細資訊，請參閱附錄 G：驅動程式方針中的[對應已淘汰](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)函式以提供回溯相容性。  
  
 當應用程式使用取代函式，而基礎*驅動程式是 ODBC 2.x*驅動程式時，驅動程式管理員會將函式呼叫對應至相對應的已被取代函數。  
  
|ODBC *2.x*函數|ODBC *3.x*函數|  
|-------------------------|-------------------------|  
|**SQLAllocConnect**|**SQLAllocHandle**|  
|**SQLAllocEnv**|**SQLAllocHandle**|  
|**SQLAllocStmt**|**SQLAllocHandle**|  
|**SQLColAttributes**|**SQLColAttribute**|  
|**SQLError**|**SQLGetDiagRec**|  
|**SQLExtendedFetch**[1]|**SQLFetchScroll**|  
|**SQLFreeConnect**|**SQLFreeHandle**|  
|**SQLFreeEnv**|**SQLFreeHandle**|  
|**SQLGetConnectOption**|**SQLGetConnectAttr**|  
|**SQLGetStmtOption**|**SQLGetStmtAttr**|  
|**SQLParamOptions**|**SQLSetStmtAttr**、 **SQLGetStmtAttr**|  
|**SQLSetConnectOption**|**SQLSetConnectAttr**|  
|**SQLSetParam**|**SQLBindParameter**|  
|**SQLSetStmtOption**|**SQLSetStmtAttr**|  
|**SQLTransact**|**SQLEndTran**|  
  
 [1] 函數**SQLExtendedFetch**是重複的功能;**SQLFetchScroll** *在 ODBC 3.x*中提供了相同的功能。 不過，在*針對 ODBC 3.x*驅動程式執行時，驅動程式管理員不會將**SQLExtendedFetch**對應至**SQLFetchScroll** 。 如需詳細資訊，請參閱「[驅動程式管理員](../../../odbc/reference/appendixes/what-the-driver-manager-does.md)」在附錄 G：驅動程式指南中提供的回溯相容性。 驅動程式管理員會在*對 ODBC 2.x*驅動程式進行**SQLFetchScroll**時，將其對應至**SQLExtendedFetch** 。  
  
> [!NOTE]
>  函數**SQLBindParam**是特殊案例。 **SQLBindParam**是重複的功能。 這不是 ODBC 2.x 函式，而是存在於開放式群組和 ISO 標準中*的函數。* 此函式所提供的功能完全由**SQLBindParameter**所建立小計。 因此，當基礎*驅動程式是 ODBC 3.x*驅動程式時，驅動程式管理員會將**SQLBindParam**的呼叫對應至**SQLBindParameter** 。 不過，當基礎*驅動程式是 ODBC 2.x*驅動程式時，驅動程式管理員不會執行此對應。
