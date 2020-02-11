---
title: 時間和日期函式（Visual FoxPro ODBC Driver） |Microsoft Docs
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
ms.openlocfilehash: 537af13edf943e27a634d3a8ba4f0f85c645251f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67912407"
---
# <a name="time-and-date-functions-visual-foxpro-odbc-driver"></a>時間和日期函式 (Visual FoxPro ODBC Driver)
下表列出 Visual FoxPro ODBC 驅動程式所支援的 ODBC 時間和日期函數;當相同函式的 Visual FoxPro 文法與 ODBC 語法不同時，會列出對等的 Visual FoxPro。  
  
|ODBC 文法|Visual FoxPro 文法|  
|------------------|---------------------------|  
|CURDATE *（）*|DATE *（）*|  
|CURTIME *（）*|時間 *（）*|  
|DAYNAME *（date_exp）*|CDOW *（date_exp）*|  
|DAYOFMONTH （*date_exp）*|DAY *（）*|  
|小時 *（time_exp）*||  
|分鐘 *（time_exp）*||  
|月份 *（time_exp）*||  
|MONTHNAME *（date_exp）*|CMONTH *（date_exp）*|  
|NOW *（）*|DATETIME *（）*|  
|SECOND *（time_exp）*|秒 *（time_exp）*|  
|周 *（date_exp）*||  
|年 *（date_exp）*||  
  
 下列時間和日期函數不受支援：  
  
 DAYOFYEAR *（date_exp）*  
  
 季 *（date_exp）*  
  
 TIMESTAMPADD *（interval，integer_exp，timestamp_exp）*  
  
 TIMESTAMPDIFF *（interval，timestamp_exp1，timestamp_exp2）*  
  
## <a name="odbc-escape-sequences"></a>ODBC 逸出序列  
 此驅動程式也支援日期和時間戳記資料的 ODBC 轉義順序。 Escape 子句語法如下所示：  
  
```  
--(*vendor(Microsoft),product(ODBC) d 'value' *)-  
--(*vendor(Microsoft),product(ODBC) ts ''value' *)-  
```  
  
 在此語法中， **d**表示*值*是*yyyy-mm-dd*格式的日期，而**ts**表示*該值*是*yyyy-mm-dd hh： mm： ss*[中的時間戳記。*f ...*]編排. 日期和時間戳記資料的縮寫語法如下：  
  
```  
{d 'value'}  
{ts 'value'}  
```  
  
 例如，下列每個語句都會在支援的 SQL UPDATE 命令中使用 date 和 timestamp 簡寫語法來更新 ALLTYPES.FROMASSEMBLY 資料表：  
  
```  
UPDATE alltypes  
   SET DAT_COL={d'1968-04-28'}  
   WHERE KEY=111  
  
UPDATE alltypes  
   SET DTI_COL={ts'1968-04-28 12:00:00'}  
   WHERE KEY=111  
```  
  
## <a name="remarks"></a>備註  
 如需有關 escape 序列的詳細資訊，請參閱 Odbc 程式設計*人員參考*中的 odbc 中的[逸出序列](../../odbc/reference/develop-app/escape-sequences-in-odbc.md)。
