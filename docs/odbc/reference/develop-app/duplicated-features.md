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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 84752b7e23c5394757764bf5ade57cb54004b01a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62943144"
---
# <a name="duplicated-features"></a>重複的功能
下列的 ODBC 2。*x*函式有重複的 ODBC 3。*x*函式。 如此一來，ODBC 2。*x* ODBC 3 中的函式已被取代。*x*。 ODBC 3。*x*函式稱為取代函式。  
  
 當應用程式會使用已被取代的 ODBC 2。*x*函式和基礎驅動程式是 ODBC 3。*x*驅動程式，驅動程式管理員會對應至相對應的取代函式的函式呼叫。 此規則唯一的例外是**SQLExtendedFetch**。 （請參閱下表的結尾註腳）。如需有關這些對應的詳細資訊，請參閱 <<c0> [ 對應已被取代的函式](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)在 < 附錄 g:為了與舊版相容的驅動程式指導方針。  
  
 當應用程式使用取代函式和基礎驅動程式為 ODBC 2。*x*驅動程式，驅動程式管理員會對應至對應已被取代的函式的函式呼叫。  
  
|ODBC 2。*x*函式|ODBC 3。*x*函式|  
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
|**SQLParamOptions**|**SQLSetStmtAttr**, **SQLGetStmtAttr**|  
|**SQLSetConnectOption**|**SQLSetConnectAttr**|  
|**SQLSetParam**|**SQLBindParameter**|  
|**SQLSetStmtOption**|**SQLSetStmtAttr**|  
|**SQLTransact**|**SQLEndTran**|  
  
 [1] 函式**SQLExtendedFetch**是重複的功能;**SQLFetchScroll**提供相同的功能，在 ODBC 3。*x*。 不過，驅動程式管理員未對應**SQLExtendedFetch**要**SQLFetchScroll**時針對 ODBC 3。*x*驅動程式。 如需詳細資訊，請參閱 <<c0> [ 驅動程式管理員的用途](../../../odbc/reference/appendixes/what-the-driver-manager-does.md)在 < 附錄 g:為了與舊版相容的驅動程式指導方針。 驅動程式管理員會將對應**SQLFetchScroll**要**SQLExtendedFetch**時針對 ODBC 2。*x*驅動程式。  
  
> [!NOTE]
>  此函式**SQLBindParam**是特殊案例。 **SQLBindParam**是重複的功能。 這不是 ODBC 2 *.x*函式，但存在於 Open Group 和 ISO 標準中的函式。 此函式所提供的功能完全納入來**SQLBindParameter**。 如此一來，驅動程式管理員會將對應的呼叫**SQLBindParam**要**SQLBindParameter**基礎驅動程式時 ODBC 3。*x*驅動程式。 不過，當基礎驅動程式是 ODBC 2 時，才 *.x*驅動程式、 驅動程式管理員不會執行這項對應。
