---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 39ebda5de5820cdfd7333ad1d0997593922e0a4f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039887"
---
# <a name="diagnostic-messages"></a>診斷訊息
診斷訊息會傳回每個的 SQLSTATE。 一些不同的訊息通常會傳回相同的 SQLSTATE。 比方說，會傳回 SQLSTATE 42000 （語法錯誤或存取違規），發生 SQL 語法的大部分錯誤。 不過，每個語法錯誤很可能由不同的訊息描述。  
  
 範例診斷訊息會列在錯誤中的資料行的資料表的每個函式和附錄 A 中的 Sqlstate。 雖然驅動程式可以傳回這些訊息，但是它們更可能會傳回任何訊息會傳遞給它們的資料來源。  
  
 應用程式通常會顯示給使用者，以及的 SQLSTATE 和原生錯誤碼的診斷訊息。 這可協助使用者和支援人員決定任何問題的原因。 內嵌在訊息中的元件資訊是在此情況下這特別有幫助。  
  
 診斷訊息是來自資料來源和 ODBC 連接，例如驅動程式、 閘道和驅動程式管理員中的元件而定。 一般而言，資料來源不直接支援 ODBC。 因此，如果從資料來源中的 ODBC 連接的元件收到訊息時，它必須識別資料來源做為訊息的來源。 它也必須識別本身做為元件收到的訊息。  
  
 如果錯誤或警告的來源元件本身，診斷訊息必須說明此點。 因此，訊息的文字有兩種不同的格式。 錯誤和警告不會發生在資料來源中，診斷訊息必須使用此格式：  
  
 **[** *vendor-identifier* **][** *ODBC-component-identifier* **]** *component-supplied-text*  
  
 錯誤和警告發生在資料來源中，診斷訊息必須使用此格式：  
  
 **[** *廠商識別碼* **] [** *ODBC 元件識別碼* **] [** *資料來源識別碼* **]** *資料來源-提供-文字*  
  
 下表顯示每個元素的意義。  
  
|項目|意義|  
|-------------|-------------|  
|*vendor-identifier*|識別發生錯誤或警告，或直接從資料來源收到的錯誤或警告之元件的廠商。|  
|*ODBC-component-identifier*|識別發生錯誤或警告，或直接從資料來源收到的錯誤或警告的元件。|  
|*data-source-identifier*|識別資料來源。 對於檔案為基礎的驅動程式，這通常是一種檔案格式，例如 Xbase [1] 的 DBMS 為基礎的驅動程式中，這是 DBMS 的產品。|  
|*component-supplied-text*|ODBC 元件所產生。|  
|*data-source-supplied-text*|產生的資料來源。|  
  
 [1] 在此情況下，驅動程式做為驅動程式和資料來源。  
  
 方括號 ( **[]** ) 必須包含在訊息，並不表示選擇性的項目。
