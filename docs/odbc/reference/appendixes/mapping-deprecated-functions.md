---
description: 對應已淘汰的函式
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
ms.openlocfilehash: 9c990646c54fd0d0698482c5f8dc3f87df80fe93
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429610"
---
# <a name="mapping-deprecated-functions"></a>對應已淘汰的函式
本節說明 ODBC 3.x 驅動程式管理員如何對應已淘汰的函式，以保證*與 odbc 2.x* *應用程式*搭配使用的 odbc *3.x 驅動程式*回溯相容性。 無論應用程式的版本為何，驅動程式管理員都會執行此對應。 由於下列清單中的每個 ODBC 2.x*函數都會*對應*到 odbc 3.x 驅動程式*中所呼叫的*對應 odbc 3.X*函式，因此 odbc 3.x 驅動程式並不需要*執行 odbc 2.x* *函數。*  
  
 當 *驅動程式是 ODBC 3.x* 驅動程式，而驅動程式不支援正在對應的函數時，就會觸發清單中的對應。  
  
 下表 *列出 ODBC 3.x*引進的所有重複功能。  
  
|ODBC *2.x* 函數|ODBC *3.x* 函數|  
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
  
 [1] *雖然 ODBC 2.x 中不*存在此函式，但它是在 Open 群組和 ISO 標準中。  
  
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
