---
title: 診斷記錄 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305179"
---
# <a name="diagnostic-records"></a>診斷記錄
與每個環境、連接、語句和描述項控制碼相關聯的是*診斷記錄*。 這些記錄包含使用特定控制碼之最後一個函式的相關診斷資訊。 只有在使用該控制碼呼叫另一個函式時，才會取代記錄。 任何一次可以儲存的診斷記錄數目並無任何限制。  
  
 有兩種類型的診斷記錄：*標頭記錄*和零或多個*狀態記錄*。 標頭記錄為記錄 0;狀態記錄為記錄1和更新版本。 診斷記錄是由數個不同的欄位所組成，標頭記錄和狀態記錄各不相同。 此外，ODBC 元件也可以定義自己的診斷記錄欄位。  
  
 雖然診斷記錄可以視為結構，但並不需要實際為結構。驅動程式儲存診斷資訊的方式是驅動程式特有的。  
  
 診斷記錄中的欄位會以**SQLGetDiagField**抓取。 您可以使用**SQLGetDiagRec**，在單一呼叫中抓取狀態記錄的 [SQLSTATE]、[原生錯誤號碼] 和 [診斷訊息] 欄位。  
  
 此章節包含下列主題。  
  
-   [標頭記錄](../../../odbc/reference/develop-app/header-record.md)  
  
-   [狀態記錄](../../../odbc/reference/develop-app/status-records.md)
