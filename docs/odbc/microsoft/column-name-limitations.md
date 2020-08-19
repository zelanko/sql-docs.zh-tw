---
description: 資料行名稱限制
title: 資料行名稱限制 |Microsoft Docs
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
ms.openlocfilehash: 82cac260fc81ce5a2cfbbe3e4c3c0bdab5a47049
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483691"
---
# <a name="column-name-limitations"></a>資料行名稱限制
資料行名稱可以包含任何有效的字元 (例如，空格) 。 如果資料行名稱包含字母、數位和底線以外的任何字元，則名稱必須以引號括住， (') 。  
  
 使用 Microsoft Access 或 Microsoft Excel 驅動程式時，資料行名稱的限制為64個字元，而較長的名稱則會產生錯誤。 使用 Paradox 驅動程式時，最大的資料行名稱為25個字元。 使用文字驅動程式時，最大的資料行名稱是64個字元，而較長的名稱則會被截斷。  
  
 使用 dBASE 驅動程式時，ASCII 值大於127的字元會轉換成底線。  
  
 使用 Microsoft Excel 驅動程式時，如果資料行名稱存在，就必須在第一個資料列中。 在 Microsoft Excel 中使用 "！" 字元的名稱，必須以引號括住 (') 。 "！" 字元會轉換成 "$" 字元，因為 "！" 字元在 ODBC 名稱中不合法，即使名稱以引號括住亦同。 除了管道字元 ( # A0) # A3 以外，其他所有有效的 Microsoft Excel 字元都 (可用於資料行名稱，包括空格。 Microsoft Excel 資料行名稱必須使用分隔識別碼來包含空格。 未指定的資料行名稱將會取代為驅動程式產生的名稱，例如，第一個資料行的 "Col1"。  
  
 無論名稱是否以引號括住， ( # A0) 不能用在資料行名稱中。  
  
 使用文字驅動程式時，如果未指定資料行名稱，驅動程式會提供預設名稱。 例如，驅動程式會呼叫第一個資料行 F1、第二個數據行 F2 等等。
