---
title: 診斷訊息 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic messages messages
- error messages [ODBC], diagnostic messages
- diagnostic messages [ODBC]
ms.assetid: 98027871-9901-476e-a722-ee58b7723c1f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9ea827e040afa43762edc32c5a4c28de5581b94e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32911303"
---
# <a name="diagnostic-messages"></a>診斷訊息
診斷訊息會傳回包含每個的 SQLSTATE。 一些不同的訊息通常會傳回相同的 SQLSTATE。 例如，SQLSTATE 42000 （語法錯誤或存取違規） 會傳回 SQL 語法中的大部分錯誤。 不過，每個語法錯誤很可能透過不同的訊息描述。  
  
 範例的診斷訊息會列在錯誤中的資料行資料表的每個函式和附錄 A 中的 Sqlstate。 雖然驅動程式可傳回這些訊息，都可能會傳回任何訊息傳遞到這些資料來源。  
  
 應用程式通常會顯示診斷訊息給使用者，以及的 SQLSTATE 和原生錯誤碼。 這可協助使用者與技術支援人員決定任何問題的原因。 訊息中的內嵌元件資訊是特別有幫助這項作業。  
  
 診斷訊息來自資料來源和 ODBC 連接，例如驅動程式、 閘道和驅動程式管理員中的元件。 一般而言，資料來源不直接支援 ODBC。 因此，如果 ODBC 連接中的元件從資料來源接收訊息時，它必須做為訊息的來源識別資料來源。 它也必須將本身視為元件收到的訊息。  
  
 如果元件本身為錯誤或警告的來源，必須說明這個診斷訊息。 因此，訊息的文字有兩種不同的格式。 錯誤和警告，不會發生在資料來源，診斷訊息必須使用以下格式：  
  
 **[** *廠商識別碼* **] [** *ODBC 元件識別碼* **]** *元件提供文字*  
  
 錯誤和警告發生在資料來源中，診斷訊息必須使用以下格式：  
  
 **[** *廠商識別碼* **] [** *ODBC 元件識別碼* **] [** *資料來源識別碼* **]** *資料來源-提供的文字*  
  
 下表顯示每個項目的意義。  
  
|元素|意義|  
|-------------|-------------|  
|*廠商識別碼*|識別發生錯誤或警告，或直接從資料來源接收錯誤或警告之元件的廠商。|  
|*ODBC 元件識別碼*|識別發生錯誤或警告，或直接從資料來源接收錯誤或警告的元件。|  
|*資料來源識別碼*|識別資料來源。 以檔案為基礎的驅動程式，這通常是檔案格式，例如 Xbase [1] 的 DBMS 架構驅動程式，這是 DBMS 的產品。|  
|*元件提供文字*|ODBC 元件所產生。|  
|*資料來源-提供的文字*|產生的資料來源。|  
  
 [1] 在此情況下，驅動程式做為驅動程式和資料來源。  
  
 方括號 (**[]**) 必須包含在訊息並不表示選擇性的項目。
