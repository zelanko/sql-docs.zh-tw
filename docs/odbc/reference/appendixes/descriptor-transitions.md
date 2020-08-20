---
description: 描述項轉換
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 168df441e2e7e785f7dfc89894ec7aa9caf8207c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456594"
---
# <a name="descriptor-transitions"></a>描述項轉換
ODBC 描述項有下列三種狀態。  
  
|State|描述|  
|-----------|-----------------|  
|D0|未配置的描述項|  
|D1i|隱含配置的描述項|  
|D1e|明確配置的描述項|  
  
 下表顯示每個 ODBC 函數如何影響描述項的狀態。  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|D0<br /><br /> 未配置|D1i<br /><br /> 隱含|D1e<br /><br /> 明確|  
|------------------------|----------------------|----------------------|  
|D1i [1]|--|--|  
|D1e [2]|--|--|  
  
 [1] 當 SQL_HANDLE_STMT *HandleType* 時，這個資料列會顯示轉換。  
  
 [2] 當 SQL_HANDLE_DESC *HandleType* 時，這個資料列會顯示轉換。  
  
## <a name="sqlcopydesc"></a>SQLCopyDesc  
  
|D0<br /><br /> 未配置|D1i<br /><br /> 隱含|D1e<br /><br /> 明確|  
|------------------------|----------------------|----------------------|  
| (IH) |--|--|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|D0<br /><br /> 未配置|D1i<br /><br /> 隱含|D1e<br /><br /> 明確|  
|------------------------|----------------------|----------------------|  
|--[1]|D0|--|  
| (IH) [2]| (HY017) |D0|  
  
 [1] 當 SQL_HANDLE_STMT *HandleType* 時，這個資料列會顯示轉換。  
  
 [2] 當 SQL_HANDLE_DESC *HandleType* 時，這個資料列會顯示轉換。  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec"></a>SQLGetDescField 和 SQLGetDescRec  
  
|D0<br /><br /> 未配置|D1i<br /><br /> 隱含|D1e<br /><br /> 明確|  
|------------------------|----------------------|----------------------|  
| (IH) |--|--|  
  
## <a name="sqlsetdescfield-and-sqlsetdescrec"></a>SQLSetDescField 和 SQLSetDescRec  
  
|D0<br /><br /> 未配置|D1i<br /><br /> 隱含|D1e<br /><br /> 明確|  
|------------------------|----------------------|----------------------|  
| (IH) [1]|--|--|  
  
 [1] 此資料列會在*DescriptorHandle*是 ARD、APD 或 IPD 的控制碼時顯示轉換，或當*DescriptorHandle* *是 IRD*的控制碼或 SQL_DESC_ROWS_PROCESSED_PTR SQL_DESC_ARRAY_STATUS_PTR 或時，顯示**SQLSetDescField**) 的 (。  
  
## <a name="all-other-odbc-functions"></a>所有其他 ODBC 函數  
  
|D0<br /><br /> 未配置|D1i<br /><br /> 隱含|D1e<br /><br /> 明確|  
|------------------------|----------------------|----------------------|  
|--|--|--|
