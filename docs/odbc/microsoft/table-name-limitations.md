---
description: 資料表名稱限制
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
ms.openlocfilehash: ef1395ab9e112e045fb90dc6f06a83b96bc48697
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471470"
---
# <a name="table-name-limitations"></a>資料表名稱限制
資料表名稱可以包含任何有效的字元 (例如，空格) 。 如果資料表名稱包含字母、數位和底線以外的任何字元，則名稱必須以引號括住， (') 。  
  
 使用 Microsoft Excel 驅動程式時，如果資料庫參考未限定資料表名稱，則會隱含預設資料庫。 如果 Microsoft Excel 中的名稱包含 "！" 字元，則會自動將它轉譯成 "$" 字元。  
  
 Microsoft excel 3.0 和4.0 檔案支援參考的 Microsoft Excel 資料表名稱 \<filename> 。 \<workbook-name>Microsoft excel 5.0、7.0 或97檔案支援參考的 Microsoft excel 資料表名稱。  
  
 使用 dBASE 驅動程式時，ASCII 值大於127的字元會轉換成底線。  
  
 使用 Microsoft Access 驅動程式時，資料表名稱的限制為64個字元。  
  
 使用 dBASE、Microsoft Excel 3.0 或4.0、Paradox 或 Text 驅動程式時，不應該使用特殊的 MS-DOS 關鍵字 CON、AUX、LPT1 和 LPT2 作為資料表名稱。
