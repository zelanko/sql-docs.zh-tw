---
title: "描述元轉換 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- state transitions [ODBC], descriptor
- transitioning states [ODBC], descriptor
- descriptor transitions [ODBC]
ms.assetid: 0cf24fe6-5e3c-45fa-81b8-4f52ddf8501d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 280d35d8ce03d3d7685441c12d99c05c9ff5f451
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="descriptor-transitions"></a>描述元轉換
ODBC 描述項會有下列三種狀態。  
  
|State|Description|  
|-----------|-----------------|  
|D0|未配置的描述元|  
|D1i|隱含地配置描述項|  
|D1e|明確配置描述項|  
  
 下表顯示每個 ODBC 函數如何影響的描述元的狀態。  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|D0<br /><br /> 未配置|D1i<br /><br /> 隱含|D1e<br /><br /> 明確|  
|------------------------|----------------------|----------------------|  
|D1i [1]|--|--|  
|D1e [2]|--|--|  
  
 [1] 這個資料列會顯示轉換時*HandleType*已 SQL_HANDLE_STMT。  
  
 [2] 這個資料列會顯示轉換時*HandleType*已 SQL_HANDLE_DESC。  
  
## <a name="sqlcopydesc"></a>SQLCopyDesc  
  
|D0<br /><br /> 未配置|D1i<br /><br /> 隱含|D1e<br /><br /> 明確|  
|------------------------|----------------------|----------------------|  
|(KARTRIS)|--|--|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|D0<br /><br /> 未配置|D1i<br /><br /> 隱含|D1e<br /><br /> 明確|  
|------------------------|----------------------|----------------------|  
|--[1]|D0|--|  
|(KARTRIS)[2]|(HY017)|D0|  
  
 [1] 這個資料列會顯示轉換時*HandleType*已 SQL_HANDLE_STMT。  
  
 [2] 這個資料列會顯示轉換時*HandleType*已 SQL_HANDLE_DESC。  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec"></a>SQLGetDescField 和 SQLGetDescRec  
  
|D0<br /><br /> 未配置|D1i<br /><br /> 隱含|D1e<br /><br /> 明確|  
|------------------------|----------------------|----------------------|  
|(KARTRIS)|--|--|  
  
## <a name="sqlsetdescfield-and-sqlsetdescrec"></a>SQLSetDescField 和 SQLSetDescRec  
  
|D0<br /><br /> 未配置|D1i<br /><br /> 隱含|D1e<br /><br /> 明確|  
|------------------------|----------------------|----------------------|  
|(KARTRIS)[1]|--|--|  
  
 [1] 這個資料列會顯示轉換時*DescriptorHandle* ARD、 APD，或 IPD，代碼或 (針對**SQLSetDescField**) 時*DescriptorHandle* IRD 的代碼和*FieldIdentifier* SQL_DESC_ARRAY_STATUS_PTR 或 SQL_DESC_ROWS_PROCESSED_PTR。  
  
## <a name="all-other-odbc-functions"></a>其他所有 ODBC 函數  
  
|D0<br /><br /> 未配置|D1i<br /><br /> 隱含|D1e<br /><br /> 明確|  
|------------------------|----------------------|----------------------|  
|--|--|--|
