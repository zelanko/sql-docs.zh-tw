---
description: 間隔常值語法
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 20a994cbcfa063a4bbc7189f95d6f7e45ba2ffb0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483251"
---
# <a name="interval-literal-syntax"></a>間隔常值語法
下列語法用於 ODBC 中的間隔常值。  
  
 *interval-literal：： = interval* [+*&#124;*-] *間隔-字串間隔-辨識符號*  
  
 *間隔-字串* ：： = *引號* { *年-月-常* 值 &#124; *日期時間-常* 值} *引號*  
  
 *年-月-常* 值：： = *年-值* &#124; [*年-值* -] *月-值*  
  
 *日期時間-常* 值：： = *日期時間間隔* &#124; *時間間隔*  
  
 *日期時間間隔* ：： = *天-值* [*小時-值* [：*分鐘-值*[：*秒-值*]]]  
  
 *時間間隔* ：： = *小時-值* [：*分鐘-值* [：*秒-值* ]]  
  
 &#124; *分鐘-值* [：*秒-值* ]  
  
 &#124; *秒-值*  
  
 year *-value* ：： = *datetime-value*  
  
 *月-值* ：： = *日期時間-值*  
  
 *days-value* ：： = *datetime-value*  
  
 *hours-value* ：： = *datetime-value*  
  
 *分鐘-value* ：： = *datetime-value*  
  
 *秒-值* ：： = *秒-整數-值* [. [*秒-分數*]]  
  
 *秒-整數-值* ：： = 不 *帶正負號的整數*  
  
 *秒-小數* ：： = 不 *帶正負號的整數*  
  
 *datetime-value* ：： = 不 *帶正負號的整數*  
  
 *間隔-辨識符號* ：： *= 開始-* 欄位至 *結束* 欄位 &#124; *單一日期時間欄位*  
  
 *開始-欄位* ：： = *非第二個日期時間欄位* [ (*間隔前置欄位-精確度* ) ]  
  
 *結束欄位* ：： = *非第二個日期時間-欄位* &#124; 第二個 [ (*間隔-小數秒-精確度*) ]  
  
 *single datetime-field* ：： = *非第二個日期時間欄位* [ (*間隔前置欄位-精確度*) ] &#124; 第二個 [ (*間隔-前置欄位-精確度* [， (*間隔-小數秒-精確度*) ]  
  
 *datetime-field* ：： = *非 second-datetime-field* &#124; second  
  
 *非第二個日期時間-field* ：： = YEAR &#124; MONTH &#124; DAY &#124; HOUR &#124; 分鐘  
  
 *間隔-小數秒-精確度* ：： = 不 *帶正負號-整數*  
  
 *間隔-前置欄位-精確度* ：： = 不 *帶正負號-整數*  
  
 *引述* ：： = '  
  
 不*帶正負號的整數*：： =*數位 ...*
