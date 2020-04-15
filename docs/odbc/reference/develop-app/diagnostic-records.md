---
title: 診斷記錄 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- handles [ODBC], diagnostic records
- header records [ODBC]
- status records [ODBC]
- diagnostic records [ODBC]
ms.assetid: 92c73f9b-3ed7-410d-9cec-2771004aae60
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b564f2837bc76e04011170e191d00c08d10c119d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305179"
---
# <a name="diagnostic-records"></a>診斷記錄
與每個環境關聯的連線、語句與描述符句柄是*診斷紀錄*。 這些記錄包含有關使用特定句柄的最後一個調用的函數的診斷資訊。 僅當使用該句柄調用另一個函數時,才會替換記錄。 任何一次可以存儲的診斷記錄數量沒有限制。  
  
 有兩種類型的診斷紀錄:*標頭記錄*與零個或多個*狀態紀錄*。 標頭記錄為記錄 0;標頭記錄為 0。狀態記錄是記錄 1 和以上。 診斷記錄由多個單獨的欄位組成,這些欄位對於標頭記錄和狀態記錄是不同的。 此外,ODBC 元件可以定義自己的診斷記錄欄位。  
  
 雖然診斷記錄可以被視為結構,但不需要它們實際上是結構;驅動程式如何存儲診斷資訊是特定於驅動程式的。  
  
 使用**SQLGetDiagField**檢索診斷記錄中的欄位。 可以使用**SQLGetDiagRec**在單個調用中檢索狀態記錄的 SQLSTATE、本機錯誤編號和診斷消息欄位。  
  
 此章節包含下列主題。  
  
-   [標頭記錄](../../../odbc/reference/develop-app/header-record.md)  
  
-   [狀態記錄](../../../odbc/reference/develop-app/status-records.md)
