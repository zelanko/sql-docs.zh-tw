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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 928e9ffa4701568aac8c519a23e7e371596a36eb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47765805"
---
# <a name="diagnostic-records"></a>診斷記錄
每個環境相關聯，連接、 陳述和描述項控制代碼所*診斷記錄*。 這些記錄包含最後一個呼叫的函式，使用特定的控制代碼相關的診斷資訊。 另一個函式呼叫使用該控制代碼時，才取代記錄。 可以一次儲存的診斷記錄的數目沒有限制。  
  
 有兩種類型的診斷記錄：*標頭記錄*以及零個或更多*狀態記錄*。 標頭記錄為記錄 0;狀態記錄為記錄 1 和更新版本。 診斷記錄是由數個不同的標頭記錄和狀態記錄的個別欄位所組成。 此外，ODBC 元件也可以定義自己的診斷記錄欄位。  
  
 雖然診斷記錄可以視為結構，但沒有需要為它們實際上是結構;驅動程式儲存的診斷資訊的方式是特定驅動程式。  
  
 在 診斷記錄的欄位會擷取與**SQLGetDiagField**。 SQLSTATE、 自發性錯誤號碼和狀態記錄的診斷訊息欄位可以使用單一呼叫中擷取**SQLGetDiagRec**。  
  
 此章節包含下列主題。  
  
-   [標頭記錄](../../../odbc/reference/develop-app/header-record.md)  
  
-   [狀態記錄](../../../odbc/reference/develop-app/status-records.md)
