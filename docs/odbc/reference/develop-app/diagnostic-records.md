---
description: 診斷記錄
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
ms.openlocfilehash: 1b407ef1f8664191a16f54942f42f4088824517c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499919"
---
# <a name="diagnostic-records"></a>診斷記錄
與每個環境、連接、語句和描述項控制碼相關聯的是 *診斷記錄*。 這些記錄包含使用特定控制碼之最後一個函式的相關診斷資訊。 只有在使用該控制碼呼叫另一個函式時，才會取代記錄。 任何一次都可以儲存的診斷記錄數目沒有任何限制。  
  
 診斷記錄有兩種類型： *標頭記錄* 和零或多個 *狀態記錄*。 標頭記錄為記錄 0;狀態記錄是記錄1和更新的記錄。 診斷記錄是由一些不同的欄位所組成，標頭記錄和狀態記錄會有所不同。 此外，ODBC 元件也可以定義自己的診斷記錄欄位。  
  
 雖然可以將診斷記錄視為結構，但它們並不需要實際為結構;驅動程式儲存診斷資訊的方式是驅動程式特定的。  
  
 診斷記錄中的欄位會以 **SQLGetDiagField**抓取。 狀態記錄的 SQLSTATE、原生錯誤號碼和診斷訊息欄位可以在使用 **SQLGetDiagRec**的單一呼叫中取出。  
  
 此章節包含下列主題。  
  
-   [標頭記錄](../../../odbc/reference/develop-app/header-record.md)  
  
-   [狀態記錄](../../../odbc/reference/develop-app/status-records.md)
