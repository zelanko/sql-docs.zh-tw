---
description: SQLGetConnectOption 函式
title: SQLGetConnectOption 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetConnectOption
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetConnectOption
helpviewer_keywords:
- SQLGetConnectOption function [ODBC]
ms.assetid: 59cde899-7957-4b5e-8677-f34d3b859bfd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: df3fd7dc9a024348c4371fabdbcabfab63a6f071
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421282"
---
# <a name="sqlgetconnectoption-function"></a>SQLGetConnectOption 函式
**一致性**  
 引進的版本： ODBC 1.0 標準合規性：已淘汰  
  
 **總結**  
 在 ODBC 3.x *中，odbc* *2.x 函數* **SQLGetConnectOption** 已被 **SQLGetConnectAttr**取代。 如需詳細資訊，請參閱 [SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)。  
  
> [!NOTE]
>  如需當 ODBC 2.x 應用程式*與 odbc 3.x* *驅動程式搭配*使用時，驅動程式管理員會將此函式對應至的詳細資訊，請參閱附錄 G：驅動程式指導方針中的[對應已淘汰](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)函式以提供回溯相容性。  
> 
> [!NOTE]
>  **SQLGetConnectOption**不支援 ODBC 3.8 中引進的屬性 SQL_ASYNC_DBC_FUNCTION_ENABLE。 在連接控制碼上使用非同步作業的應用程式必須使用 **SQLGetConnectAttr**。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
