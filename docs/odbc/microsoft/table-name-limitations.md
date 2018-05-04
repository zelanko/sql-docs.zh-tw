---
title: 資料表名稱限制 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, table name limitations
- table name limitations [ODBC]
- Excel driver [ODBC], table name limitations
ms.assetid: d9843e4b-1d05-4d5a-9dc3-ee9ec59edb97
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8ffba1295cf16c48402987165e90c61bc9c5cc65
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="table-name-limitations"></a>資料表名稱限制
資料表名稱可以包含任何有效的字元 （例如，空格）。 如果資料表名稱可以包含字母、 數字和底線以外的任何字元，名稱必須括在後引號 （'） 分隔。  
  
 當使用 Microsoft Excel 驅動程式時，資料庫參考不限定資料表名稱，就會隱含的預設資料庫。 如果在 Microsoft Excel 中的名稱包含"！"字元，它將自動轉譯成"$"字元改為。  
  
 Microsoft Excel 資料表名稱參考\<檔名 > 支援 Microsoft Excel 3.0 和 4.0 的檔案。 Microsoft Excel 資料表名稱參考\<活頁簿名稱 > 支援的 Microsoft Excel 5.0、 7.0、 或 97 檔案。  
  
 使用 dBASE 驅動程式時，就會將使用 ASCII 值大於 127 的字元轉換成底線。  
  
 使用 Microsoft Access 驅動程式時，資料表名稱會僅限於 64 個字元。  
  
 使用 dBASE，Microsoft Excel 3.0 或 4.0，Paradox 或文字驅動程式時，特殊 MS-DOS 關鍵字 CON、 AUX、 LPT1、 和 LPT2 不應做為資料表名稱。
