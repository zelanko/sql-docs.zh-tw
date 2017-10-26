---
title: "資料行名稱限制 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- desktop database drivers [ODBC], column names
- ODBC desktop database drivers [ODBC], column names
ms.assetid: 5a339f61-c52f-40ad-8deb-d785f72753d4
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a5e2fb7cf9f54177ce357058e51e541b6a442379
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="column-name-limitations"></a>資料行名稱限制
資料行名稱可以包含任何有效的字元 （例如，空格）。 如果資料行名稱可以包含字母、 數字和底線以外的任何字元，名稱必須括在後引號 （'） 分隔。  
  
 使用 Microsoft Access 或 Microsoft Excel 驅動程式時，資料行名稱限制為 64 個字元，且更長的名稱產生錯誤。 使用 Paradox 驅動程式時，最大資料行名稱會是 25 個字元。 使用文字驅動程式時，最大資料行名稱為 64 個字元，並會被截斷較長的名稱。  
  
 使用 dBASE 驅動程式時，就會將使用 ASCII 值大於 127 的字元轉換成底線。  
  
 使用 Microsoft Excel 驅動程式時，如果資料行名稱存在，它們必須是第一列。 在 Microsoft Excel 中會使用名稱"！"字元必須括在後引號 （'）。 "！"字元轉換成"$"字元，因為"！"字元以回復括住的名稱，即使是不合法的 ODBC 名稱中。 其他有效的 Microsoft Excel 字元 (除非縱線字元 (&#124;)) 可用資料行的名稱，包括空格。 分隔的識別碼必須用 Microsoft Excel 的資料行名稱，來加上空格。 未指定資料行名稱會取代驅動程式產生的名稱，例如，"Col1"的第一個資料行。  
  
 縱線字元 (&#124;) 不能在資料行名稱是否或不以回復括住名稱。  
  
 使用文字驅動程式時，驅動程式會提供預設名稱，如果未指定資料行名稱。 例如，驅動程式會呼叫第一個資料行 F1、 F2，第二個資料行等等。

