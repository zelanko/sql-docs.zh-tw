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
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47694049"
---
# <a name="interval-literal-syntax"></a>間隔常值語法
下列語法用於 ODBC 中的間隔常值。  
  
 *間隔常值:: = 間隔*[+*&#124;*-]*間隔字串間隔限定詞*  
  
 *時間間隔字串*:: =*報價*{*年-月-l* &#124; *日期時間常值*}*報價*  
  
 *年-月-l* :: =*年份值* &#124; [*年份值*-]*月份值*  
  
 *日期時間常值*:: =*天的時間間隔* &#124; *時間間隔*  
  
 *日期時間間隔*:: =*天數值*[*小時值*[:*分鐘值*[:*秒數值*]]]  
  
 *時間間隔*:: =*小時值*[:*分鐘值*[:*秒數值*]]  
  
 &#124;*分鐘的時間值*[:*秒數值*]  
  
 &#124;*秒數值*  
  
 *年份值*:: =*日期時間值*  
  
 *月數值*:: =*日期時間值*  
  
 *天數值*:: =*日期時間值*  
  
 *小時值*:: =*日期時間值*  
  
 *分鐘值*:: =*日期時間值*  
  
 *秒數值*:: =*秒的整數值*[。 [*小數秒*]]  
  
 *秒數的整數值*:: =*不帶正負號整數*  
  
 *小數秒*:: =*不帶正負號整數*  
  
 *日期時間值*:: =*不帶正負號整數*  
  
 *間隔限定詞*:: =*開始欄位*TO*結尾欄位* &#124; *單一日期時間欄位*  
  
 *開始欄位*:: =*非秒-datetime-欄位*[(*間隔業界-欄位精確度*)]  
  
 *結束欄位*:: =*非秒-datetime-欄位*&#124;第二個 [(*間隔小數-秒的有效位數*)]  
  
 *單一日期時間欄位*:: =*非秒-datetime-欄位*[(*間隔業界-欄位精確度*)]&#124;第二個 [(*間隔業界欄位-精確度* [，(*間隔小數-秒的有效位數*)]  
  
 *日期時間欄位*:: =*非秒-datetime-欄位*&#124;第二個  
  
 *非秒-datetime-欄位*:: = 年&#124;月&#124;天&#124;小時&#124;分鐘  
  
 *間隔-分-秒數-有效位數*:: =*不帶正負號整數*  
  
 *間隔開頭-欄位精確度*:: =*不帶正負號整數*  
  
 *引號*:: = '  
  
 *不帶正負號整數*:: =*數字...*
