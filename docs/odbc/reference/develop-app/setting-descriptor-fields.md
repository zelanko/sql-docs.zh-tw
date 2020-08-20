---
description: 設定描述項欄位
title: 設定描述項欄位 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], retrieving or setting field values
ms.assetid: d735dc64-370f-48ab-a59f-6cef9bc4e1e8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6625db69709098f3a3db1a1d40f9ab583eee4030
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476430"
---
# <a name="setting-descriptor-fields"></a>設定描述項欄位
若要修改描述項的欄位，應用程式可以呼叫 **SQLSetDescField**。 某些欄位是唯讀的，無法設定。  (參閱 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) 函式描述。 )   
  
 描述項記錄欄位是以記錄號碼 (*RecNumber*) 為1或更高，而描述項標頭欄位是以0的記錄號碼來設定。 記錄號碼0也會用來設定書簽欄位，根據書簽包含在資料行0的慣例。 這可能會讓您覺得書簽欄位包含在描述項標頭中，但不是這樣。 書簽欄位與標頭欄位不同。  
  
 個別設定欄位時，應用程式應該遵循 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)中定義的順序。 設定某些欄位會導致驅動程式設定其他欄位。 這樣可確保在應用程式指定資料類型之後，描述項隨時都可以使用。 當應用程式設定 SQL_DESC_TYPE 欄位時，驅動程式會檢查指定類型的其他欄位是否有效且一致。  
  
 如果設定描述項欄位的函式呼叫失敗，則在失敗的函式呼叫之後，描述項欄位的內容會未定義。
