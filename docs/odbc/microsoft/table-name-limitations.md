---
title: 表名稱限制 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 738c563961eae56471f0238d9726a1ebb0bdc76e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81289214"
---
# <a name="table-name-limitations"></a>資料表名稱限制
表名稱可以包含任何有效的字元(例如空格)。 如果表名稱包含除字母、數位和下劃線以外的任何字元,則必須通過在後引號 (') 中括起來來分隔名稱。  
  
 當使用 Microsoft Excel 驅動程式,並且資料庫引用不限定表名稱時,隱含默認資料庫。 如果 Microsoft Excel 中的名稱包含"!"字元,則該名稱將自動轉換為"$"字元。  
  
 Microsoft Excel 3.0\<和 4.0 檔案支援引用檔名>的 Microsoft Excel 表名。 Microsoft Excel 5.0、7.0 或 97\<個檔支援引用 工作簿名稱>的 Microsoft Excel 表名稱。  
  
 使用 dBASE 驅動程式時,ASCII 值大於 127 的字元將轉換為下劃線。  
  
 使用 Microsoft Access 驅動程式時,表名稱限制為 64 個字元。  
  
 當使用 dBASE、Microsoft Excel 3.0 或 4.0、Paradox 或文本驅動程式時,不應將特殊的 MS-DOS 關鍵字 CON、AUX、LPT1 和 LPT2 用作表名。
