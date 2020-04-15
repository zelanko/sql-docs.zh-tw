---
title: SQLGetConnectOption 功能 |微軟文件
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
ms.openlocfilehash: 94a29637365862990ea067f663023fae04a7af3e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285568"
---
# <a name="sqlgetconnectoption-function"></a>SQLGetConnectOption 函式
**一致性**  
 版本介紹: ODBC 1.0 標準合規性: 已棄用  
  
 **摘要**  
 在 ODBC *3.x*中,ODBC *2.x*函數**SQLGetConnectOption**已被**SQLGetConnectAttr**替換。 有關詳細資訊,請參閱[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)。  
  
> [!NOTE]
>  有關驅動程式管理員將此功能映射到 ODBC *2.x*應用程式使用 ODBC *3.x*驅動程式時的詳細資訊,請參閱附錄 G:向後相容性驅動程式指南中的[對應已棄用函數](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)。  
> 
> [!NOTE]
>  **SQLGetConnectOption**不支援在 ODBC 3.8 中引入的屬性SQL_ASYNC_DBC_FUNCTION_ENABLE。 在連接句柄上使用非同步操作的應用程式必須使用**SQLGetConnectAttr**。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
