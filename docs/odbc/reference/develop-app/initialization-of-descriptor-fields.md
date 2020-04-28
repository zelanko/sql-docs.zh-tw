---
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
ms.openlocfilehash: e4ed6479a60f1d0695107c216b2f0c94a55f68ff
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300118"
---
# <a name="initialization-of-descriptor-fields"></a>描述項欄位的初始設定
配置應用程式資料列描述項時，其欄位會接收如[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)中所示的初始值。 SQL_DESC_TYPE 欄位的初始值為 SQL_DEFAULT。 這可提供資料庫資料的標準處理方式，以便呈現給應用程式。 應用程式可以藉由設定描述項記錄的欄位，來指定不同的資料處理方式。  
  
 描述項標頭中 SQL_DESC_ARRAY_SIZE 的初始值為1。 應用程式可以修改此欄位，以啟用多資料列提取。  
  
 預設值的概念對於 IRD 的欄位而言是不正確。 只有在有已備妥或已執行的語句與其相關聯時，應用程式才能取得 IRD 的欄位存取權。  
  
 IPD 的特定欄位只有在 IPD 已由驅動程式自動填入後才會定義。 如果不是，則為未定義。 這些欄位是 SQL_DESC_CASE_SENSITIVE、SQL_DESC_FIXED_PREC_SCALE、SQL_DESC_TYPE_NAME、SQL_DESC_UNSIGNED 和 SQL_DESC_LOCAL_TYPE_NAME。
