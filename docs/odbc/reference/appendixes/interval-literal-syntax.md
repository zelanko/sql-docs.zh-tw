---
title: 間隔常值語法 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- literals [ODBC], interval
- interval literals [ODBC]
- ODBC literals [ODBC], interval
ms.assetid: 2f2d22c1-51d6-4055-9f5a-53bc31e9fea0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d477dbc6b54d7ebd82b7e2ef8611f5f6dd807e83
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63188822"
---
# <a name="interval-literal-syntax"></a>間隔常值語法
下列語法用於 ODBC 中的間隔常值。  
  
 *interval-literal ::= INTERVAL* [+ *&#124;* -] *interval-string interval-qualifier*  
  
 *interval-string* ::= *quote* { *year-month-literal* &#124; *day-time-literal* } *quote*  
  
 *year-month-literal* ::= *years-value* &#124; [*years-value* -] *months-value*  
  
 *day-time-literal* ::= *day-time-interval* &#124; *time-interval*  
  
 *day-time-interval* ::= *days-value* [*hours-value* [:*minutes-value*[:*seconds-value*]]]  
  
 *time-interval* ::= *hours-value* [:*minutes-value* [:*seconds-value* ] ]  
  
 &#124; *minutes-value* [:*seconds-value* ]  
  
 &#124; *seconds-value*  
  
 *years-value* ::= *datetime-value*  
  
 *months-value* ::= *datetime-value*  
  
 *days-value* ::= *datetime-value*  
  
 *hours-value* ::= *datetime-value*  
  
 *minutes-value* ::= *datetime-value*  
  
 *seconds-value* ::= *seconds-integer-value* [.[*seconds-fraction*] ]  
  
 *seconds-integer-value* ::= *unsigned-integer*  
  
 *seconds-fraction* ::= *unsigned-integer*  
  
 *datetime-value* ::= *unsigned-integer*  
  
 *interval-qualifier* ::= *start-field* TO *end-field* &#124; *single-datetime-field*  
  
 *start-field* ::= *non-second-datetime-field* [(*interval-leading-field-precision* )]  
  
 *end-field* ::= *non-second-datetime-field* &#124; SECOND[(*interval-fractional-seconds-precision*)]  
  
 *單一日期時間欄位*:: =*非秒-datetime-欄位*[(*間隔業界-欄位精確度*)]&#124;第二個 [(*間隔業界欄位-精確度* [，(*間隔小數-秒的有效位數*)]  
  
 *datetime-field* ::= *non-second-datetime-field* &#124; SECOND  
  
 *非秒-datetime-欄位*:: = 年&#124;月&#124;天&#124;小時&#124;分鐘  
  
 *interval-fractional-seconds-precision* ::= *unsigned-integer*  
  
 *interval-leading-field-precision* ::= *unsigned-integer*  
  
 *quote* ::= '  
  
 *unsigned-integer* ::= *digit...*
