---
title: 時間和日期功能(可視化福克斯Pro ODBC驅動程式) |微軟文件
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
ms.openlocfilehash: 86260f8e7245bed15122d4dbfc4649131674e17f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303059"
---
# <a name="time-and-date-functions-visual-foxpro-odbc-driver"></a>時間和日期函式 (Visual FoxPro ODBC Driver)
下表列出了 Visual FoxPro ODBC 驅動程式支援的 ODBC 時間和日期函數;當相同函數的 Visual FoxPro 語法與 ODBC 語法不同時,將列出 Visual FoxPro 等效項。  
  
|ODBC 語法|視覺化 FoxPro 語法|  
|------------------|---------------------------|  
|CURDATE *( )*|日期 *( )*|  
|CURTIME *( )*|時間 *( )*|  
|天名 *(date_exp)*|CDOW *(date_exp)*|  
|一月 *(date_exp日)*|日 *( )*|  
|小時 *(time_exp)*||  
|分鐘 *(time_exp)*||  
|月 *(time_exp)*||  
|月名稱 *(date_exp)*|CMONTH *(date_exp)*|  
|現在 *( )*|日期時間 *( )*|  
|秒 *(time_exp)*|SEC *(time_exp)*|  
|週 *(date_exp)*||  
|年份 *(date_exp)*||  
  
 不支援以下時間與日期函數:  
  
 一天 *(date_exp)*  
  
 *(date_exp)*  
  
 時間戳(*間隔、integer_exp、timestamp_exp)*  
  
 時間戳 *(間隔、timestamp_exp1、timestamp_exp2)*  
  
## <a name="odbc-escape-sequences"></a>ODBC 逸出序列  
 驅動程式還支援日期和時間戳數據的 ODBC 轉義序列。 逸出子句語法如下所示:  
  
```  
--(*vendor(Microsoft),product(ODBC) d 'value' *)-  
--(*vendor(Microsoft),product(ODBC) ts ''value' *)-  
```  
  
 在此文法中 **,d**指示*值*是*yyyy-mm-dd*格式的日期 **,ts**表示*值*是*yyyy-mm-dhh:mm:ss*中的時間戳 。*f...* 格式。 日期和時間戳資料的速記語法如下所示:  
  
```  
{d 'value'}  
{ts 'value'}  
```  
  
 例如,以下每個語句都使用受支援的 SQL UPDATE 命令中的日期和時間戳速記語法更新 ALLTYPES 表:  
  
```  
UPDATE alltypes  
   SET DAT_COL={d'1968-04-28'}  
   WHERE KEY=111  
  
UPDATE alltypes  
   SET DTI_COL={ts'1968-04-28 12:00:00'}  
   WHERE KEY=111  
```  
  
## <a name="remarks"></a>備註  
 有關逸出序列的詳細資訊,請參閱*ODBC 程式者參考*[中的 ODBC 中的逸出序列](../../odbc/reference/develop-app/escape-sequences-in-odbc.md)。
