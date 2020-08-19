---
description: SQLTransact 函式
title: SQLTransact 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLTransact
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLTransact
helpviewer_keywords:
- SQLTransact function [ODBC]
ms.assetid: 496249e0-8eff-4c60-8358-5543bc3ead9c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 35eb9ff0a59d1b11838c1b74f8b229ce324f9e94
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421032"
---
# <a name="sqltransact-function"></a>SQLTransact 函式
**一致性**  
 引進的版本： ODBC 1.0 標準合規性：已淘汰  
  
 **總結**  
 在 ODBC 3.x *中，odbc* *2.x 函數* **SQLTransact** 已被 **SQLEndTran**取代。 如需詳細資訊，請參閱 [SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)。  
  
> [!NOTE]  
>  **SQLTransact**不支援在 ODBC 3.8 中引進的屬性 SQL_ASYNC_DBC_FUNCTION_ENABLE。 在連接控制碼上使用非同步作業的應用程式必須使用 **SQLEndTran**。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
