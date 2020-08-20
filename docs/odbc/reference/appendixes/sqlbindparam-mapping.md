---
description: SQLBindParam 對應
title: SQLBindParam 對應 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBindparam function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLBindParam
ms.assetid: 375f8f24-36de-4946-916e-c75abc6f070d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f998fd30716e479cb4dd0650af53c5a24483f2f5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456459"
---
# <a name="sqlbindparam-mapping"></a>SQLBindParam 對應
**SQLBindParam** 無法真正被取代為已淘汰，因為它永遠不會存在於 ODBC 中;不過，它仍代表重複的功能-驅動程式管理員需要將它匯出，因為 ISO 和開放式群組相容的應用程式將會使用它。 由於**SQLBindParameter**包含**SQLBindParam**的所有功能，因此當基礎*驅動程式是 ODBC 3.x*驅動程式) 時， **SQLBindParam**將會在**SQLBindParameter** (上對應。 *ODBC 3.x*驅動程式不需要執行**SQLBindParam**。  
  
## <a name="remarks"></a>備註  
 進行下列 **SQLBindParam** 呼叫時：  
  
```  
SQLBindParam(   StatementHandle,    ParameterNumber,    ValueType,    ParameterType,    ColumnSize,    DecimalDigits,    ParameterValuePtr,    StrLen_or_IndPtr)  
```  
  
 驅動程式管理員會在驅動程式中呼叫 **SQLBindParameter** ，如下所示：  
  
```  
SQLBindParameter(   StatementHandle,    ParameterNumber,    SQL_PARAM_INPUT,    ValueType,    ParameterType,    ColumnSize,    DecimalDigits,    ParameterValuePtr,    BufferLength,    StrLen_or_IndPtr)  
```  
  
 如果您的應用程式將在64位作業系統上執行，請參閱 [ODBC 64 位資訊](../../../odbc/reference/odbc-64-bit-information.md)。  
  
## <a name="see-also"></a>另請參閱  
 [對應已被取代的函式](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)
