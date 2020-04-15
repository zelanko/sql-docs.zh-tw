---
title: 延遲欄位 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], deferred fields
- deferred fields [ODBC]
ms.assetid: 5abeb9cc-4070-4f43-a80d-ad6a2004e5f3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 094aba353e10ed568e1959b1d655109296507dee
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305969"
---
# <a name="deferred-fields"></a>延遲的欄位
設置*延遲欄位*時不使用這些值,但驅動程式會保存變數的位址以執行延遲效果。 對於應用程式參數描述符,驅動程式在調用**SQLExecDirect**或**SQLExecute**時使用變數的內容。 對於應用程式行描述符,驅動程式在提取時使用變數的內容。  
  
 以下是遞延欄位:  
  
-   描述符記錄的SQL_DESC_DATA_PTR欄位和SQL_DESC_INDICATOR_PTR欄位。  
  
-   應用程式描述符記錄的SQL_DESC_OCTET_LENGTH_PTR欄位。  
  
-   在多行提取的情況下,SQL_DESC_ARRAY_STATUS_PTR和SQL_DESC_ROWS_PROCESSED_PTR描述符標頭的欄位。  
  
 分配描述符時,每個描述符記錄的遞延欄位最初具有 null 值。 null 值的含義如下:  
  
-   如果SQL_DESC_ARRAY_STATUS_PTR值為空,則多行提取無法返回每行診斷資訊的此元件。  
  
-   如果SQL_DESC_DATA_PTR為 null 值,則記錄將未綁定。  
  
-   如果ARD的SQL_DESC_OCTET_LENGTH_PTR欄位具有空值,則驅動程式不會返回該列的長度資訊。  
  
-   如果 APD 的SQL_DESC_OCTET_LENGTH_PTR字段具有空值,並且參數是字串,則驅動程式假定字串為 null 終止。 對於輸出動態參數,此欄位中的空值可防止驅動程式返回長度資訊。 (如果SQL_DESC_TYPE欄位不指示字元字串參數,則忽略SQL_DESC_OCTET_LENGTH_PTR欄位。  
  
 應用程式不得在將延遲欄位與欄位關聯到驅動程式讀取或寫入這些欄位的時間之間解調或丟棄用於延遲欄位的變數。
