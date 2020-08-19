---
description: 描述項欄位的初始設定
title: 描述項欄位的初始化 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], allocating and freeing
- initializing descriptor fields [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 1da157cb-8ea9-4a56-983b-1c45650217c5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2537e5e74c600c72368e46bda7640b881d9a34df
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424650"
---
# <a name="initialization-of-descriptor-fields"></a>描述項欄位的初始設定
配置應用程式資料列描述項時，其欄位會接收 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)中指出的初始值。 SQL_DESC_TYPE 欄位的初始值為 SQL_DEFAULT。 這可提供資料庫資料的標準處理，以呈現給應用程式。 應用程式可以藉由設定描述項記錄的欄位，來指定不同的資料處理方式。  
  
 描述項標頭中 SQL_DESC_ARRAY_SIZE 的初始值為1。 應用程式可以修改此欄位，以啟用多資料列提取。  
  
 預設值的概念對 IRD 的欄位無效。 只有當已備妥或已執行的語句與其相關聯時，應用程式才能取得 IRD 欄位的存取權。  
  
 只有在驅動程式自動填入 IPD 之後，才會定義 IPD 的某些欄位。 如果沒有，則未定義。 這些欄位為 SQL_DESC_CASE_SENSITIVE、SQL_DESC_FIXED_PREC_SCALE、SQL_DESC_TYPE_NAME、SQL_DESC_UNSIGNED 和 SQL_DESC_LOCAL_TYPE_NAME。
