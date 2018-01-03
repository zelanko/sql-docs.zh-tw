---
title: "時間和日期函式 （Visual FoxPro ODBC 驅動程式） |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC date functions [ODBC]
- Visual FoxPro ODBC driver [ODBC], time and date functions
- FoxPro ODBC driver [ODBC], time and date functions
- time and date functions [ODBC]
- ODBC time and date functions [ODBC]
- date functions [ODBC]
ms.assetid: c1fb63b7-af50-45d6-8dec-ae6ea7119527
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 95545399054e35ee9377f2be5ad2569205c64e8b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="time-and-date-functions-visual-foxpro-odbc-driver"></a>時間和日期函式 （Visual FoxPro ODBC 驅動程式）
下表列出 Visual FoxPro ODBC 驅動程式; 支援 ODBC 時間和日期函數當相同的函式的 Visual FoxPro 文法與 ODBC 語法，會列出 Visual FoxPro 相等。  
  
|ODBC 文法|Visual FoxPro 文法|  
|------------------|---------------------------|  
|CURDATE*（)*|日期*（)*|  
|CURTIME*（)*|時間*（)*|  
|DAYNAME*(date_exp)*|CDOW*(date_exp)*|  
|DAYOFMONTH (*date_exp)*|天*（)*|  
|小時*(time_exp)*||  
|分鐘*(time_exp)*||  
|月份*(time_exp)*||  
|MONTHNAME*(date_exp)*|CMONTH*(date_exp)*|  
|現在*（)*|DATETIME*（)*|  
|第二個*(time_exp)*|秒*(time_exp)*|  
|週*(date_exp)*||  
|年份*(date_exp)*||  
  
 不支援下列日期和時間函數：  
  
 DAYOFYEAR *(date_exp)*  
  
 季*(date_exp)*  
  
 TIMESTAMPADD*間隔、 integer_exp (timestamp_exp）*  
  
 TIMESTAMPDIFF*間隔、 timestamp_exp1 (timestamp_exp2）*  
  
## <a name="odbc-escape-sequences"></a>ODBC 逸出序列  
 驅動程式也支援 ODBC 逸出序列的日期和時間戳記資料。 逸出子句語法如下所示：  
  
```  
--(*vendor(Microsoft),product(ODBC) d 'value' *)—  
--(*vendor(Microsoft),product(ODBC) ts ''value' *)—  
```  
  
 在此語法中， **d**表示*值*是中的日期*yyyy-mm-dd*格式和**ts**表示*值*是時間戳記在*yyyy-mm-dd hh: mm:*[。*f...*] 格式。 日期和時間戳記資料的速記語法如下所示：  
  
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
 如需逸出序列的詳細資訊，請參閱[ODBC 中的逸出序列](../../odbc/reference/develop-app/escape-sequences-in-odbc.md)中*ODBC 程式設計人員參考*。
