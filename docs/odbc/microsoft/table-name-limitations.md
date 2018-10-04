---
title: 資料表名稱限制 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, table name limitations
- table name limitations [ODBC]
- Excel driver [ODBC], table name limitations
ms.assetid: d9843e4b-1d05-4d5a-9dc3-ee9ec59edb97
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 31c1703bc03a2881e7b9b96989b8949cc81aba7b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47707046"
---
# <a name="table-name-limitations"></a>資料表名稱限制
資料表名稱可以包含任何有效的字元 （例如空格）。 如果資料表名稱可以包含字母、 數字和底線以外的任何字元，必須括在後引號 （'） 分隔名稱。  
  
 當使用 Microsoft Excel 驅動程式時，資料庫參考不限定資料表名稱，就會隱含的預設資料庫。 如果在 Microsoft Excel 中的名稱包含"！"字元，它將會自動會轉譯成"$"字元改。  
  
 Microsoft Excel 資料表名稱參考\<檔案名稱 > 支援 Microsoft Excel 3.0 和 4.0 的檔案。 Microsoft Excel 資料表名稱參考\<活頁簿名稱 > 支援 Microsoft Excel 5.0、 7.0、 或 97 檔案。  
  
 使用 dBASE 驅動程式時，使用 ASCII 值大於 127 的字元會轉換成底線。  
  
 使用 Microsoft Access 驅動程式時，資料表名稱僅限於 64 個字元。  
  
 使用 dBASE，也就是 3.0 或 4.0，Paradox 或文字的 Microsoft Excel 驅動程式時，f，AUX、 LPT1、 LPT2 特殊的 MS-DOS 關鍵字不應為資料表名稱。
