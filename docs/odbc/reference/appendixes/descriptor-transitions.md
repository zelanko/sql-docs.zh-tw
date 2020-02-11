---
title: 描述項轉換 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 44e9d92c7371451d6bfdd2e1513c3f8fdac8447b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68130004"
---
# <a name="descriptor-transitions"></a>描述項轉換
ODBC 描述元具有下列三種狀態。  
  
|State|描述|  
|-----------|-----------------|  
|D0|未配置的描述元|  
|D1i|隱含配置的描述元|  
|D1e|明確配置的描述元|  
  
 下表顯示每個 ODBC 函數如何影響描述項狀態。  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|D0<br /><br /> 未配置|D1i<br /><br /> 隱含|D1e<br /><br /> 明確|  
|------------------------|----------------------|----------------------|  
|D1i [1]|--|--|  
|D1e [2]|--|--|  
  
 [1] 當 SQL_HANDLE_STMT *HandleType*時，此資料列會顯示轉換。  
  
 [2] 當 SQL_HANDLE_DESC *HandleType*時，此資料列會顯示轉換。  
  
## <a name="sqlcopydesc"></a>SQLCopyDesc  
  
|D0<br /><br /> 未配置|D1i<br /><br /> 隱含|D1e<br /><br /> 明確|  
|------------------------|----------------------|----------------------|  
|(IH)|--|--|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|D0<br /><br /> 未配置|D1i<br /><br /> 隱含|D1e<br /><br /> 明確|  
|------------------------|----------------------|----------------------|  
|--[1]|D0|--|  
|(IH)2|(HY017)|D0|  
  
 [1] 當 SQL_HANDLE_STMT *HandleType*時，此資料列會顯示轉換。  
  
 [2] 當 SQL_HANDLE_DESC *HandleType*時，此資料列會顯示轉換。  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec"></a>SQLGetDescField 和 SQLGetDescRec  
  
|D0<br /><br /> 未配置|D1i<br /><br /> 隱含|D1e<br /><br /> 明確|  
|------------------------|----------------------|----------------------|  
|(IH)|--|--|  
  
## <a name="sqlsetdescfield-and-sqlsetdescrec"></a>SQLSetDescField 和 SQLSetDescRec  
  
|D0<br /><br /> 未配置|D1i<br /><br /> 隱含|D1e<br /><br /> 明確|  
|------------------------|----------------------|----------------------|  
|(IH)sha-1|--|--|  
  
 [1] 當*DescriptorHandle*是 ARD、APD 或 IPD 的控制碼時，或（若為**SQLSetDescField**），當*DescriptorHandle*為 IRD 和*FieldIdentifier*的控制碼 SQL_DESC_ARRAY_STATUS_PTR 或 SQL_DESC_ROWS_PROCESSED_PTR 時，此資料列會顯示轉換。  
  
## <a name="all-other-odbc-functions"></a>所有其他 ODBC 函數  
  
|D0<br /><br /> 未配置|D1i<br /><br /> 隱含|D1e<br /><br /> 明確|  
|------------------------|----------------------|----------------------|  
|--|--|--|
