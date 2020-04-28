---
title: 對應已淘汰的函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], about mapping deprecated functions
- backward compatibility [ODBC], mapping deprecated functions
- deprecated functions [ODBC]
- compatibility [ODBC], mapping deprecated functions
- functions [ODBC], mapping deprecated functions
- mapping deprecated functions [ODBC]
ms.assetid: ee462617-1d79-4c88-afeb-b129cff34cc6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a4e89cd9281520e70ec5fb289c6050e77ec6194c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299878"
---
# <a name="mapping-deprecated-functions"></a>對應已淘汰的函式
本節說明 ODBC 3.x 驅動程式管理員如何對應已淘汰的函式，以確保*與 odbc 2.x* *應用程式*搭配使用的 odbc *3.x 驅動程式*具有回溯相容性。 無論應用程式的版本為何，驅動程式管理員都會執行此對應。 由於下列清單中的每個 ODBC 2.x 函數在 ODBC 3.x 驅動程式中呼叫時，都會對應到相對應的 ODBC 3.x 函式，因此，ODBC 3.x*驅動程式不*需要*2.x*執行 odbc 2.x *3.x* *函數。* *2.x*  
  
 當*驅動程式是 ODBC 3.x*驅動程式，而驅動程式不支援正在對應的函式時，就會觸發清單中的對應。  
  
 下表*列出 ODBC 3.x*中引進的所有重複功能。  
  
|ODBC *2.x*函數|ODBC *3.x*函數|  
|-------------------------|-------------------------|  
|**SQLAllocConnect**|**SQLAllocHandle**|  
|**SQLAllocEnv**|**SQLAllocHandle**|  
|**SQLAllocStmt**|**SQLAllocHandle**|  
|**SQLBindParam**[1]|**SQLBindParameter**|  
|**SQLColAttributes**|**SQLColAttribute**|  
|**SQLError**|**SQLGetDiagRec**|  
|**SQLFreeConnect**|**SQLFreeHandle**|  
|**SQLFreeEnv**|**SQLFreeHandle**|  
|具有 SQL_DROP*選項*的**SQLFreeStmt**|**SQLFreeHandle**|  
|**SQLGetConnectOption**|**SQLGetConnectAttr**|  
|**SQLGetStmtOption**|**SQLGetStmtAttr**|  
|**SQLParamOptions**|**SQLSetStmtAttr**|  
|**SQLSetConnectOption**|**SQLSetConnectAttr**|  
|**SQLSetParam**[2]|**SQLBindParameter**|  
|**SQLSetScrollOption**|**SQLSetStmtAttr**|  
|**SQLSetStmtOption**|**SQLSetStmtAttr**|  
|**SQLTransact**|**SQLEndTran**|  
  
 [1] 即使此函式不存在*于 ODBC 2.x 中，* 它仍是開放式群組和 ISO 標準。  
  
 [2] 這是 ODBC 1.0 函數。  
  
 此章節包含下列主題。  
  
-   [SQLAllocConnect 對應](../../../odbc/reference/appendixes/sqlallocconnect-mapping.md)  
  
-   [SQLAllocEnv 對應](../../../odbc/reference/appendixes/sqlallocenv-mapping.md)  
  
-   [SQLAllocStmt 對應](../../../odbc/reference/appendixes/sqlallocstmt-mapping.md)  
  
-   [SQLBindParam 對應](../../../odbc/reference/appendixes/sqlbindparam-mapping.md)  
  
-   [SQLColAttributes 對應](../../../odbc/reference/appendixes/sqlcolattributes-mapping.md)  
  
-   [SQLError 對應](../../../odbc/reference/appendixes/sqlerror-mapping.md)  
  
-   [SQLFreeConnect 對應](../../../odbc/reference/appendixes/sqlfreeconnect-mapping.md)  
  
-   [SQLFreeEnv 對應](../../../odbc/reference/appendixes/sqlfreeenv-mapping.md)  
  
-   [SQLFreeStmt 對應](../../../odbc/reference/appendixes/sqlfreestmt-mapping.md)  
  
-   [SQLGetConnectOption 對應](../../../odbc/reference/appendixes/sqlgetconnectoption-mapping.md)  
  
-   [SQLGetStmtOption 對應](../../../odbc/reference/appendixes/sqlgetstmtoption-mapping.md)  
  
-   [SQLInstallTranslator 對應](../../../odbc/reference/appendixes/sqlinstalltranslator-mapping.md)  
  
-   [SQLParamOptions 對應](../../../odbc/reference/appendixes/sqlparamoptions-mapping.md)  
  
-   [SQLSetConnectOption 對應](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md)  
  
-   [SQLSetParam 對應](../../../odbc/reference/appendixes/sqlsetparam-mapping.md)  
  
-   [SQLSetScrollOptions 對應](../../../odbc/reference/appendixes/sqlsetscrolloptions-mapping.md)  
  
-   [SQLSetStmtOption 對應](../../../odbc/reference/appendixes/sqlsetstmtoption-mapping.md)  
  
-   [SQLTransact 對應](../../../odbc/reference/appendixes/sqltransact-mapping.md)
