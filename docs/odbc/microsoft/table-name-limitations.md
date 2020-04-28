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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 738c563961eae56471f0238d9726a1ebb0bdc76e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81289214"
---
# <a name="table-name-limitations"></a>資料表名稱限制
資料表名稱可以包含任何有效的字元（例如空格）。 如果資料表名稱包含字母、數位和底線以外的任何字元，則必須將其括在後引號（'）中，以分隔名稱。  
  
 使用 Microsoft Excel 驅動程式時，如果資料表名稱不是由資料庫參考所限定，則會隱含使用預設資料庫。 如果 Microsoft Excel 中的名稱包含 "！" 字元，則會自動將它轉譯成 "$" 字元。  
  
 Microsoft Excel 3.0 和4.0 檔案支援\<參考 filename> 的 microsoft excel 資料表名稱。 Microsoft Excel 5.0、7.0 或 97 \<檔案支援參考活頁簿名稱> 的 microsoft excel 資料表名稱。  
  
 使用 dBASE 驅動程式時，ASCII 值大於127的字元會轉換成底線。  
  
 使用 Microsoft Access 驅動程式時，資料表名稱會限制為64個字元。  
  
 當使用 dBASE、Microsoft Excel 3.0 或4.0、Paradox 或文字驅動程式時，特殊的 MS-DOS 關鍵字 CON、AUX、LPT1 和 LPT2 不應當做資料表名稱使用。
