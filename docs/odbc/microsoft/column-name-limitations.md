---
title: 資料行名稱的限制 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8a80ed397ae494bc686ef76aaeeef10b61662f19
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63301804"
---
# <a name="column-name-limitations"></a>資料行名稱限制
資料行名稱可以包含任何有效的字元 （例如空格）。 如果資料行名稱可包含字母、 數字和底線以外的任何字元，必須括在後引號 （'） 分隔名稱。  
  
 使用 Microsoft Access 或 Microsoft Excel 驅動程式時，資料行名稱限制為 64 個字元，且更長的名稱會產生錯誤。 使用 Paradox 驅動程式時，最大資料行名稱會是 25 個字元。 使用文字驅動程式時，最大資料行名稱是 64 個字元，而較長的名稱會被截斷。  
  
 使用 dBASE 驅動程式時，使用 ASCII 值大於 127 的字元會轉換成底線。  
  
 使用 Microsoft Excel 驅動程式時，資料行名稱是否存在於，它們必須在第一個資料列。 也可以使用這個在 Microsoft Excel 中的名稱"！"字元必須括在後引號 （'）。 "！"字元轉換成"$"字元，因為"！"字元是不合法在 ODBC 名稱，即使以後引號括住名稱。 其他有效的 Microsoft Excel 字元 (除非直立線符號字元 (&#124;)) 可用於資料行名稱，包括空格。 分隔的識別碼必須用於 Microsoft Excel 的資料行名稱，要加上空格。 未指定的資料行名稱將會取代驅動程式產生的名稱，例如，"Col1"的第一個資料行。  
  
 直立線符號字元 (&#124;) 不能在資料行名稱，是否以後括住名稱。  
  
 使用文字驅動程式時，此驅動程式會提供預設名稱，如果未指定資料行名稱。 例如，驅動程式會呼叫第一個資料行 F1、 f2 鍵，第二個資料行等等。
