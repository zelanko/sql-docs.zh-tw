---
title: 時間和日期函式 (Visual FoxPro ODBC Driver) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7752c1c1d5184ddb1beea26d7c35e29ea5769796
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47644326"
---
# <a name="time-and-date-functions-visual-foxpro-odbc-driver"></a>時間和日期函式 (Visual FoxPro ODBC Driver)
下表列出支援的 Visual FoxPro ODBC Driver; ODBC 日期和時間函數當相同的函式的 Visual FoxPro 文法與 ODBC 語法，會列出 Visual FoxPro 相等。  
  
|ODBC 文法|Visual FoxPro 文法|  
|------------------|---------------------------|  
|CURDATE *（)*|日期 *（)*|  
|CURTIME *（)*|時間 *（)*|  
|DAYNAME *(date_exp)*|CDOW *(date_exp)*|  
|DAYOFMONTH (*date_exp)*|天 *（)*|  
|小時 *(time_exp)*||  
|分鐘 *(time_exp)*||  
|月 *(time_exp)*||  
|MONTHNAME *(date_exp)*|CMONTH *(date_exp)*|  
|現在 *（)*|DATETIME *（)*|  
|第二個 *(time_exp)*|秒 *(time_exp)*|  
|週 *(date_exp)*||  
|年 *(date_exp)*||  
  
 不支援下列的日期和時間函數：  
  
 DAYOFYEAR *(date_exp)*  
  
 季 *(date_exp)*  
  
 TIMESTAMPADD*間隔、 integer_exp (timestamp_exp）*  
  
 TIMESTAMPDIFF*間隔、 timestamp_exp1 (timestamp_exp2）*  
  
## <a name="odbc-escape-sequences"></a>ODBC 逸出序列  
 驅動程式也支援 ODBC 逸出序列的日期和時間戳記資料。 逸出子句語法如下所示：  
  
```  
--(*vendor(Microsoft),product(ODBC) d 'value' *)—  
--(*vendor(Microsoft),product(ODBC) ts ''value' *)—  
```  
  
 在這個語法中， **d**指出*值*是中的日期*yyyy-mm-dd 的-* 格式和**ts**表示*值*是在一個時間戳記*yyyy 為 yyyy-mm-dd hh: mm:*[。*f...*] 格式。 日期和時間戳記資料的速記語法如下所示：  
  
```  
{d 'value'}  
{ts 'value'}  
```  
  
 例如，以下陳述式的每個更新 ALLTYPES 資料表支援的 SQL UPDATE 命令中使用的日期和時間戳記的速記語法：  
  
```  
UPDATE alltypes  
   SET DAT_COL={d'1968-04-28'}  
   WHERE KEY=111  
  
UPDATE alltypes  
   SET DTI_COL={ts'1968-04-28 12:00:00'}  
   WHERE KEY=111  
```  
  
## <a name="remarks"></a>備註  
 如需詳細資訊逸出序列的詳細資訊，請參閱[ODBC 中的逸出序列](../../odbc/reference/develop-app/escape-sequences-in-odbc.md)中*ODBC 程式設計人員參考*。
