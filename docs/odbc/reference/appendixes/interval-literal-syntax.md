---
title: 間隔文字語法 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81290568"
---
# <a name="interval-literal-syntax"></a>間隔常值語法
以下語法用於 ODBC 中的間隔文字。  
  
 *間隔文字 ::* INTERVAL* =*&#124;*-]*間隔-字串間隔限定符號*  
  
 *間隔字串*::**報價*=*年月文字*&#124;*日時文字*=*報價*  
  
 *年月文字*::**年值*&#124; =*年值*-=*月值*  
  
 *日間文字*:::**日時間隔*&#124;*時間間隔*  
  
 *時間隔*::**天值*=*小時值*[:*分鐘值*]:*秒值**  
  
 *時間間隔*::**小時值*[:*分鐘值*[:*秒值*]  
  
 &#124;*分鐘值*[:*秒值*]  
  
 &#124;*秒值*  
  
 *年值*::**日期時間值*  
  
 *月值*::**日期時間值*  
  
 *天值*::**日期時間值*  
  
 *小時值*::**日期時間值*  
  
 *分鐘值*::**日期時間值*  
  
 *秒值*::=*秒-整數值*[.]*秒數分數*|]  
  
 *秒-整數值*::**無符號整數*  
  
 *秒數分數*::**無符號整數*  
  
 *日期時間值*::**無符號整數*  
  
 *間隔限定 ::***起始欄位*到*結束欄位*&#124;*單日期時間欄位*  
  
 *起始字段*::**非秒日期時間欄位*[(*間隔前導場精度*)]  
  
 *結束欄位*::**非秒日期時間欄位*&#124;秒精度】(*間隔-分數-秒精度*)]  
  
 *單日期時間欄位*::**非秒日期時間場*[(*間隔前導場精度*)] &#124;* * *interval-fractional-seconds-precision*  
  
 *日期時間欄位*::**非秒日期時間欄位*&#124;  
  
 *非秒日期時間欄位*::* &#124;月份 &#124; 天 &#124; HOUR &#124; 分鐘  
  
 *間隔分數-秒-精度*::**無符號整數*  
  
 *間隔領先的場精度*::**無符號整數*  
  
 *報價*::*  
  
 *無符號整數*::**數位...*
