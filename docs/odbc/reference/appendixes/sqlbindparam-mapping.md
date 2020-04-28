---
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
ms.openlocfilehash: c1df595722297c91dc75398470912188e109e278
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305438"
---
# <a name="sqlbindparam-mapping"></a>SQLBindParam 對應
**SQLBindParam**無法真正被稱為「已淘汰」，因為它從未出現在 ODBC 中;不過，它仍然代表重複的功能-驅動程式管理員需要將它匯出，因為 ISO 和開放式群組相容的應用程式將會使用它。 由於**SQLBindParameter**包含**SQLBindParam**的所有功能，因此**SQLBindParam**會對應到**SQLBindParameter**之上（當基礎*驅動程式是 ODBC 3.x*驅動程式時）。 *ODBC 3.x*驅動程式不需要執行**SQLBindParam**。  
  
## <a name="remarks"></a>備註  
 對**SQLBindParam**進行下列呼叫時：  
  
```  
SQLBindParam(   StatementHandle,    ParameterNumber,    ValueType,    ParameterType,    ColumnSize,    DecimalDigits,    ParameterValuePtr,    StrLen_or_IndPtr)  
```  
  
 驅動程式管理員會呼叫驅動程式中的**SQLBindParameter** ，如下所示：  
  
```  
SQLBindParameter(   StatementHandle,    ParameterNumber,    SQL_PARAM_INPUT,    ValueType,    ParameterType,    ColumnSize,    DecimalDigits,    ParameterValuePtr,    BufferLength,    StrLen_or_IndPtr)  
```  
  
 如果您的應用程式將在64位作業系統上執行，請參閱[ODBC 64 位資訊](../../../odbc/reference/odbc-64-bit-information.md)。  
  
## <a name="see-also"></a>另請參閱  
 [對應已被取代的函式](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)
