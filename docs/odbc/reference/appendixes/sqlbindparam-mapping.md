---
title: SQLBindParam Mapping | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ecec6116ee16f4affa615518a690d2c665648464
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68091242"
---
# <a name="sqlbindparam-mapping"></a>SQLBindParam 對應
**SQLBindParam**無法真正呼叫已被取代因為它永遠不會那里在 ODBC; 不過，它仍代表重複的功能-驅動程式管理員必須將它匯出，因為 ISO 和開啟群組符合規範的應用程式將會使用它。 因為**SQLBindParameter**包含的所有功能**SQLBindParam**， **SQLBindParam**將對應的**SQLBindParameter**(當基礎驅動程式是 ODBC *3.x*驅動程式)。 ODBC *3.x*驅動程式不需要實作**SQLBindParam**。  
  
## <a name="remarks"></a>備註  
 當下列呼叫來**SQLBindParam**進行：  
  
```  
SQLBindParam(   StatementHandle,    ParameterNumber,    ValueType,    ParameterType,    ColumnSize,    DecimalDigits,    ParameterValuePtr,    StrLen_or_IndPtr)  
```  
  
 此驅動程式管理員會呼叫**SQLBindParameter**在驅動程式中，如下所示：  
  
```  
SQLBindParameter(   StatementHandle,    ParameterNumber,    SQL_PARAM_INPUT,    ValueType,    ParameterType,    ColumnSize,    DecimalDigits,    ParameterValuePtr,    BufferLength,    StrLen_or_IndPtr)  
```  
  
 請參閱[ODBC 64 位元資訊](../../../odbc/reference/odbc-64-bit-information.md)，如果您的應用程式會在 64 位元作業系統上執行。  
  
## <a name="see-also"></a>另請參閱  
 [對應已被取代的函式](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)
