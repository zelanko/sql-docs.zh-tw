---
description: 時間和日期函式 (Visual FoxPro ODBC Driver)
title: 日期和時間函式 (Visual FoxPro ODBC Driver) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC date functions [ODBC]
- Visual FoxPro ODBC driver [ODBC], time and date functions
- FoxPro ODBC driver [ODBC], time and date functions
- time and date functions [ODBC]
- ODBC time and date functions [ODBC]
- date functions [ODBC]
ms.assetid: c1fb63b7-af50-45d6-8dec-ae6ea7119527
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d537411481a8bc6c9065e8e86c216c8c0637e565
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500071"
---
# <a name="time-and-date-functions-visual-foxpro-odbc-driver"></a>時間和日期函式 (Visual FoxPro ODBC Driver)
下表列出 Visual FoxPro ODBC 驅動程式所支援的 ODBC 時間和日期函數;當相同函式的 Visual FoxPro 文法與 ODBC 語法不同時，會列出 Visual FoxPro 對等專案。  
  
|ODBC 文法|Visual FoxPro 文法|  
|------------------|---------------------------|  
|CURDATE* ( ) *|日期* ( ) *|  
|CURTIME* ( ) *|時間* ( ) *|  
|DAYNAME* (date_exp) *|CDOW* (date_exp) *|  
|DAYOFMONTH (*date_exp) *|天* ( ) *|  
|*Time_exp) *的小時 (||  
|分鐘* (time_exp) *||  
|月* (time_exp) *||  
|MONTHNAME* (date_exp) *|CMONTH* (date_exp) *|  
|現在* ( ) *|DATETIME* ( ) *|  
|第二* (time_exp) *|SEC* (time_exp) *|  
|* (date_exp) *的周||  
|YEAR* (date_exp) *||  
  
 以下是不支援的時間和日期函數：  
  
 DAYOFYEAR * (date_exp) *  
  
 季 * (date_exp) *  
  
 TIMESTAMPADD * (間隔、integer_exp timestamp_exp) *  
  
 TIMESTAMPDIFF * (間隔、timestamp_exp1 timestamp_exp2) *  
  
## <a name="odbc-escape-sequences"></a>ODBC 逸出序列  
 驅動程式也支援日期和時間戳記資料的 ODBC escape 序列。 Escape 子句語法如下所示：  
  
```  
--(*vendor(Microsoft),product(ODBC) d 'value' *)-  
--(*vendor(Microsoft),product(ODBC) ts ''value' *)-  
```  
  
 在此語法中， **d** 表示 *值* 是 *yyyy-mm-dd* 格式的日期，而 **ts** 表示 *值* 是 *yyyy-mm-dd hh： mm： ss*[中的時間戳記。*f ...*]格式。 日期和時間戳記資料的速記語法如下所示：  
  
```  
{d 'value'}  
{ts 'value'}  
```  
  
 例如，下列每個語句都會使用支援的 SQL UPDATE 命令中的日期和時間戳記速記語法來更新 ALLTYPES.FROMASSEMBLY 資料表：  
  
```  
UPDATE alltypes  
   SET DAT_COL={d'1968-04-28'}  
   WHERE KEY=111  
  
UPDATE alltypes  
   SET DTI_COL={ts'1968-04-28 12:00:00'}  
   WHERE KEY=111  
```  
  
## <a name="remarks"></a>備註  
 如需有關 escape 序列的詳細資訊，請參閱 odbc 程式設計*人員參考*中 odbc 中的[escape 序列](../../odbc/reference/develop-app/escape-sequences-in-odbc.md)。
