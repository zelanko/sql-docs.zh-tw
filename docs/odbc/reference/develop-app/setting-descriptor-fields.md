---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 34c4a6e3d98b6711c77fb50d7156207de148881a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68094249"
---
# <a name="setting-descriptor-fields"></a>設定描述項欄位
若要修改描述項的欄位，應用程式可以呼叫**SQLSetDescField**。 有些欄位是唯讀的，而且無法設定。 （請參閱[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)函數描述）。  
  
 描述項記錄欄位是以1或更高的記錄號碼（*RecNumber*）設定，而描述項標頭欄位則是以0的記錄號碼來設定。 記錄號碼0也會用來設定書簽欄位，這是根據書簽包含在資料行0中的慣例。 這可能會讓您覺得書簽欄位包含在描述元標頭中，但這不是這種情況。 書簽欄位與標頭欄位不同。  
  
 個別設定欄位時，應用程式應遵循[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)中定義的順序。 設定某些欄位會導致驅動程式設定其他欄位。 這可確保在應用程式指定資料類型後，描述項一律可供使用。 當應用程式設定 [SQL_DESC_TYPE] 欄位時，驅動程式會檢查指定類型的其他欄位是否有效且一致。  
  
 如果會設定描述項欄位的函式呼叫失敗，則描述元欄位的內容會在失敗函數呼叫之後未定義。
