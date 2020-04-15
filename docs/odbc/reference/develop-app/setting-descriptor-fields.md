---
title: 設定描述符位 ( 1) :微軟文件
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
ms.openlocfilehash: 04f9520e2ef462df481bb104e389aeb57b5dd457
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304149"
---
# <a name="setting-descriptor-fields"></a>設定描述項欄位
要修改描述符號, 應用程式可以呼叫**SQLSetDescField**。 某些欄位是唯讀的,無法設置。 (請參閱[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)函數說明。  
  
 描述符記錄欄位的設定紀錄編號 (*RecNumber*) 為 1 或更高,而描述符標頭欄位的設定記錄數為 0。 記錄數為 0 也用於設置書簽欄欄位,根據第 0 列中包含的書籤的約定。 這可能會給人留下書籤欄位包含在描述符標頭中的印象,但事實並非如此。 書籤欄位與標題欄位不同。  
  
 單獨設置欄位時,應用程式應遵循[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)中定義的順序。 設置某些欄位會導致驅動程式設置其他欄位。 這可確保描述符始終準備好在應用程式指定數據類型后使用。 當應用程式設置SQL_DESC_TYPE欄位時,驅動程式會檢查指定類型的其他欄位是否有效且一致。  
  
 如果將設置描述符位的函數調用失敗,則描述符欄位的內容在函數調用失敗後未定義。
