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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3387b07a8e769206a6a495addff4287000691fec
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81290568"
---
# <a name="interval-literal-syntax"></a>間隔常值語法
下列語法用於 ODBC 中的間隔常值。  
  
 *間隔-常值：： = interval* [+*&#124;*-]*間隔-字串間隔-限定詞*  
  
 *interval-string* ：： =*引號*{*年-月-常*值 &#124;*日期時間-常*值}*引號*  
  
 *年-月-常*值：： =*年-值*&#124; [*年-值*-]*月份-值*  
  
 *日期時間-常*值：： =*日期時間間隔*&#124;*時間間隔*  
  
 *日-時間間隔*：： =*天-值*[*小時-值*[：*分鐘-值*[：*秒數-值*]]]  
  
 *時間間隔*：： =*小時-值*[：*分鐘-值*[：*秒-值*]]  
  
 &#124;*分鐘-值*[：*秒-值*]  
  
 &#124;*秒-值*  
  
 *年-值*：： = *datetime-value*  
  
 *月份-值*：： = *datetime-value*  
  
 *days-value* ：： = *datetime-value*  
  
 *小時-值*：： = *datetime-value*  
  
 *分鐘-value* ：： = *datetime-value*  
  
 *秒-值*：： =*秒-整數-值*[. [*秒數-小數*]]  
  
 *秒-整數-值*：： = 不*帶正負號整數*  
  
 *秒數-小數*：： = 不*帶正負號-整數*  
  
 *datetime-value* ：： = 不*帶正負號整數*  
  
 *interval-辨識符號*：： *= 起始欄位*到*結束欄位*&#124;*單一日期時間-欄位*  
  
 *起始欄位*：： =*非第二個-日期時間-欄位*[（*間隔-前置欄位精確度*）]  
  
 *結尾欄位*：： =*非第二個-datetime-field* &#124; second [（*間隔-小數-秒-精確度*）]  
  
 *單一 datetime-field* ：： =*非第二個-datetime 欄位*[（*間隔-前置欄位精確度*）] &#124; 秒 [（*間隔-前置欄位精確度*[，（*間隔-小數秒數-精確度*）]  
  
 *datetime-field* ：： =*非秒-datetime-field* &#124; second  
  
 *非第二個-datetime-field* ：： = YEAR &#124; 月份 &#124; DAY &#124; 小時 &#124; 分鐘  
  
 *間隔-小數-秒-* 有效位數：： = 不*帶正負號-整數*  
  
 *間隔-前置-欄位精確度*：： = 不*帶正負號-整數*  
  
 *報價*：： = '  
  
 不*帶正負號的整數*：： =*數位 ...*
