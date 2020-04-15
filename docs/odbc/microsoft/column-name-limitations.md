---
title: 列名稱限制 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- desktop database drivers [ODBC], column names
- ODBC desktop database drivers [ODBC], column names
ms.assetid: 5a339f61-c52f-40ad-8deb-d785f72753d4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 41d973afdac360af114da41620997cad23a2c740
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281378"
---
# <a name="column-name-limitations"></a>資料行名稱限制
列名稱可以包含任何有效的字元(例如空格)。 如果列名稱包含除字母、數位和下劃線以外的任何字元,則必須通過在後引號 (') 中括起來來分隔名稱。  
  
 使用 Microsoft Access 或 Microsoft Excel 驅動程式時,列名限制為 64 個字元,較長的名稱將生成錯誤。 使用悖論驅動程式時,最大列名稱為 25 個字元。 使用 Text 驅動程式時,最大列名稱為 64 個字元,並截斷較長的名稱。  
  
 使用 dBASE 驅動程式時,ASCII 值大於 127 的字元將轉換為下劃線。  
  
 使用 Microsoft Excel 驅動程式時,如果存在列名稱,它們必須位於第一行中。 Microsoft Excel 中將使用"!" 字元的名稱必須包含在後引號 (') 中。 "!" 字元轉換為"$"字元,因為"! 所有其他有效的 Microsoft Excel 字元(管道字元(&#124;)除外)都可以在列名稱中使用,包括空格。 必須為 Microsoft Excel 列名稱使用分隔識別碼才能包含空格。 未指定的列名稱將替換為驅動程式生成的名稱,例如,第一列的"Col1"。  
  
 無論名稱是否包含在後引號中,都不能在列名稱中使用管道字元 (&#124;)。  
  
 使用 Text 驅動程式時,如果未指定列名稱,則驅動程式提供預設名稱。 例如,驅動程式調用第一列 F1、第二列 F2 等。
