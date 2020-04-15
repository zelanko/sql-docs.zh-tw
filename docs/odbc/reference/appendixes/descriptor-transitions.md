---
title: 描述符轉換 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- state transitions [ODBC], descriptor
- transitioning states [ODBC], descriptor
- descriptor transitions [ODBC]
ms.assetid: 0cf24fe6-5e3c-45fa-81b8-4f52ddf8501d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ec5c26bdde8a0d470f2d93e753504bf1c51edcc0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307039"
---
# <a name="descriptor-transitions"></a>描述項轉換
ODBC 描述符具有以下三種狀態。  
  
|State|描述|  
|-----------|-----------------|  
|D0|未配置的描述子|  
|D1i|隱含配置的描述|  
|D1e|明確配置的描述|  
  
 下表顯示了每個 ODBC 函數如何影響描述符狀態。  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|D0<br /><br /> 未配置|D1i<br /><br /> 隱含|D1e<br /><br /> 明確|  
|------------------------|----------------------|----------------------|  
|D1i[1]|--|--|  
|D1e[2]|--|--|  
  
 [1] 此行顯示*處理類型*SQL_HANDLE_STMT時的過渡。  
  
 [2] 此行顯示*handleType* SQL_HANDLE_DESC時的過渡。  
  
## <a name="sqlcopydesc"></a>SQLCopyDesc  
  
|D0<br /><br /> 未配置|D1i<br /><br /> 隱含|D1e<br /><br /> 明確|  
|------------------------|----------------------|----------------------|  
|(IH)|--|--|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|D0<br /><br /> 未配置|D1i<br /><br /> 隱含|D1e<br /><br /> 明確|  
|------------------------|----------------------|----------------------|  
|--[1]|D0|--|  
|(IH)[2]|(HY017)|D0|  
  
 [1] 此行顯示*處理類型*SQL_HANDLE_STMT時的過渡。  
  
 [2] 此行顯示*handleType* SQL_HANDLE_DESC時的過渡。  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec"></a>SQLGetDescField 和 SQLGetDescRec  
  
|D0<br /><br /> 未配置|D1i<br /><br /> 隱含|D1e<br /><br /> 明確|  
|------------------------|----------------------|----------------------|  
|(IH)|--|--|  
  
## <a name="sqlsetdescfield-and-sqlsetdescrec"></a>SQLSetDescField 和 SQLSetDescRec  
  
|D0<br /><br /> 未配置|D1i<br /><br /> 隱含|D1e<br /><br /> 明確|  
|------------------------|----------------------|----------------------|  
|(IH)[1]|--|--|  
  
 [1] 當*描述符句柄*是 ARD、APD 或 IPD 的句柄時,或者(對於**SQLSetDescField)** 的*句柄是*IRD 的句柄,*字段標識符*是SQL_DESC_ARRAY_STATUS_PTR或SQL_DESC_ROWS_PROCESSED_PTR時,此行顯示過渡。  
  
## <a name="all-other-odbc-functions"></a>所有其他 ODBC 功能  
  
|D0<br /><br /> 未配置|D1i<br /><br /> 隱含|D1e<br /><br /> 明確|  
|------------------------|----------------------|----------------------|  
|--|--|--|
