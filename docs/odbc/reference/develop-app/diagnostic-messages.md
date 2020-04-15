---
title: 診斷消息 |微軟文件
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
ms.openlocfilehash: be63e9d78960e40ac5e9ee016d2cfd868d99a922
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305829"
---
# <a name="diagnostic-messages"></a>診斷訊息
每個 SQLSTATE 都會返回一條診斷消息。 相同的 SQLSTATE 通常傳回與許多不同的訊息。 例如,SQLSTATE 42000(語法錯誤或訪問衝突)返回,用於 SQL 語法中的大多數錯誤。 但是,每個語法錯誤可能由不同的消息描述。  
  
 範例診斷訊息列在附錄 A 和每個函數中的 SQLStatEs 表中的「錯誤」列中。 儘管驅動程式可以返回這些消息,但它們更有可能返回數據源傳遞給它們的任何消息。  
  
 應用程式通常向使用者顯示診斷訊息以及 SQLSTATE 和本機錯誤代碼。 這有助於使用者和支持人員確定任何問題的原因。 消息中嵌入的元件資訊在執行此操作時特別有用。  
  
 診斷消息來自 ODBC 連接中的數據源和元件,如驅動程式、閘道和驅動程式管理器。 通常,數據源不直接支援ODBC。 因此,如果 ODBC 連接中的元件從數據來源接收消息,則必須將數據源標識為消息的來源。 它還必須將自己標識為接收消息的元件。  
  
 如果錯誤或警告的來源是元件本身,診斷消息必須解釋這一點。 因此,消息的文本有兩種不同的格式。 對於資料來源中未發生的錯誤和警告,診斷訊息必須使用此格式:  
  
 **(***供應商識別碼***) +** *ODBC-元件識別碼* **=** *元件提供文字*  
  
 對於資料來源中發生的錯誤和警告,診斷訊息必須使用此格式:  
  
 **(** *供應商識別碼* **] [** *ODBC-元件識別子***] 資料來源***識別碼* **=** *資料來源提供文字*  
  
 下表顯示了每個元素的含義。  
  
|項目|意義|  
|-------------|-------------|  
|*供應商識別碼*|標識發生錯誤或警告或直接從數據源接收錯誤或警告的元件的供應商。|  
|*ODBC 元件識別碼*|識別發生錯誤或警告或直接從數據源接收錯誤或警告的元件。|  
|*資料來源識別碼*|標識數據源。 對於基於檔的驅動程式,這通常是檔案格式,例如 Xbase{1} 對於基於 DBMS 的驅動程式,這是 DBMS 產品。|  
|*元件提供文字*|由 ODBC 元件產生。|  
|*資料來源提供文字*|由數據源生成。|  
  
 [1] 在這種情況下,驅動程式同時充當驅動程式和數據源。  
  
 括號 (*** )** 必須包含在消息中,並且不指示可選項。
