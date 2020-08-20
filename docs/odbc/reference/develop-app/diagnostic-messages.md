---
description: 診斷訊息
title: 診斷訊息 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic messages messages
- error messages [ODBC], diagnostic messages
- diagnostic messages [ODBC]
ms.assetid: 98027871-9901-476e-a722-ee58b7723c1f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6d788a8bb23b7b63ae65a6fcf8c119110b5e6557
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461510"
---
# <a name="diagnostic-messages"></a>診斷訊息
每個 SQLSTATE 會傳回一則診斷訊息。 相同的 SQLSTATE 通常會以數個不同的訊息傳回。 例如，針對 SQL 語法中的大部分錯誤，會傳回 SQLSTATE 42000 (語法錯誤或存取違規) 。 不過，每個語法錯誤可能會由不同的訊息描述。  
  
 診斷訊息範例會列在附錄 A 和每個函式中 SQLSTATEs 資料表的 [錯誤] 資料行中。 雖然驅動程式可以傳回這些訊息，但它們更可能會傳回資料來源傳遞給它們的任何訊息。  
  
 應用程式通常會向使用者顯示診斷訊息，以及 SQLSTATE 和原生錯誤碼。 這可協助使用者和支援人員判斷任何問題的原因。 內嵌在訊息中的元件資訊在執行這項操作時特別有用。  
  
 診斷訊息來自 ODBC 連接中的資料來源和元件，例如驅動程式、閘道和驅動程式管理員。 一般而言，資料來源不會直接支援 ODBC。 因此，如果 ODBC 連接中的元件接收來自資料來源的訊息，它就必須將資料來源識別為訊息的來源。 它也必須將本身識別為接收訊息的元件。  
  
 如果錯誤或警告的來源是元件本身，則診斷訊息必須說明這一點。 因此，訊息的文字有兩種不同的格式。 若為數據源中不發生的錯誤和警告，診斷訊息必須使用此格式：  
  
 **[** *廠商識別碼* **] [** *ODBC-元件識別碼* **]** *元件提供的文字*  
  
 針對資料來源中發生的錯誤和警告，診斷訊息必須使用此格式：  
  
 **[** *廠商識別碼* **] [** *ODBC-元件識別碼* **] [** *資料來源識別碼* **]** *資料來源-提供的文字*  
  
 下表顯示每個元素的意義。  
  
|元素|意義|  
|-------------|-------------|  
|*廠商識別碼*|識別發生錯誤或警告，或是直接從資料來源接收錯誤或警告之元件的廠商。|  
|*ODBC-元件識別碼*|識別發生錯誤或警告的元件，或是直接從資料來源接收錯誤或警告的元件。|  
|*資料來源識別碼*|識別資料來源。 針對以檔案為基礎的驅動程式，這通常是檔案格式，例如以 DBMS 為基礎的驅動程式的 Xbase [1]，這是 DBMS 產品。|  
|*元件提供的文字*|由 ODBC 元件產生。|  
|*資料來源提供-文字*|由資料來源產生。|  
  
 [1] 在這種情況下，驅動程式會當做驅動程式和資料來源。  
  
 訊息中必須包含括弧 (**[]**) ，而且不表示選擇性的專案。
