---
title: SQLConfigDataSource （Paradox 驅動程式） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLConfigDataSource
ms.assetid: 59e84c4e-debe-49d7-b97b-84c736b0c793
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 33cc778d921b90a460dab6bda352fd7627d2cf7b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68054068"
---
# <a name="sqlconfigdatasource-paradox-driver"></a>SQLConfigDataSource (Paradox 驅動程式)
> [!NOTE]  
>  本主題提供 Paradox 驅動程式特有的資訊。 如需此函數的一般資訊，請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)底下的適當主題。  
  
 用來以動態方式加入、修改或刪除資料來源的**SQLConfigDataSource**函數會使用下列關鍵字。  
  
|關鍵字|描述|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|排序欄位的順序。<br /><br /> 使用 Paradox 驅動程式時，順序可以是 ASCII （預設值）、國際、瑞典文、芬蘭文或挪威文-丹麥文。<br /><br /> 這會在 [安裝程式] 對話方塊中，將相同的選項設定為 [**排序次序**]。|  
|DBQ|資料庫檔案的名稱。<br /><br /> 這會在 [安裝程式] 對話方塊中設定與**資料庫**相同的選項。|  
|DEFAULTDIR|目錄的路徑規格。|  
|描述|資料來源中的資料描述。<br /><br /> 這會在 [安裝程式] 對話方塊中設定與 [**描述**] 相同的選項。|  
|DRIVER|驅動程式 DLL 的路徑規格。|  
|DRIVERID|驅動程式的整數識別碼。<br /><br /> 26（Paradox 3.x）<br /><br /> 282（Paradox 4.x）<br /><br /> 538（Paradox 5.x）|  
|獲得|判斷資料庫是否會以獨佔模式開啟（一次只能由一個使用者存取）或共用模式（一次由一個以上的使用者存取）。 可以是 true （獨佔模式）或 false （共用模式）。<br /><br /> 這會在 [安裝程式] 對話方塊中，將相同的選項設定為 [**獨佔**]。|  
|FIL|檔案類型 Paradox 7.x、Paradox 4.x 或 Paradox 5。x|  
|類型|文字驅動程式的檔案類型（文字）。|  
|PAGETIMEOUT|指定在移除之前，頁面（如果未使用）會保留在緩衝區中的一段時間，以十分之一秒為限。 預設值為600十分之一秒（60秒）。 請注意，此選項適用于使用 ODBC 驅動程式的所有資料來源。<br /><br /> 這會設定與 [設定] 對話方塊中**頁面超時**相同的選項。|  
|PARADOXNETPATH|包含 Paradox 鎖定資料庫之目錄的完整路徑，因為它包含 PDOXUSRS.net 檔案（在 Paradox 4 中）。*x*）或 PARADOX.net 檔案（在 PARADOX 5 中。*x*）。 如果目錄不包含這些檔案的其中一個，則 Paradox 驅動程式會建立一個。 如需這些檔案的詳細資訊，請參閱 Paradox 檔。<br /><br /> 您必須先輸入 Paradox 使用者名稱，才可選取網路目錄。<br /><br /> 這會設定與 [設定] 對話方塊中的 [**選取網路目錄**] 相同的選項。|  
|PARADOXNETSTYLE|若是 Paradox 驅動程式，存取 Paradox 資料時要使用的網路存取樣式： "3.x" 代表 Paradox 3。*x*或 "4. x" 的 Paradox 為4。*x*或5。*x*。 如果版本是 Paradox 4，可以設定為 "3. x" 或 "4.x"。*x*或5。*x*;如果版本是 Paradox 3，則為。*x*，樣式必須是 "3. x"。<br /><br /> 這會在 [安裝] 對話方塊中設定與**Net Style**相同的選項。|  
|PARADOXUSERNAME|若是 Paradox 驅動程式，Paradox 的使用者名稱。<br /><br /> 這會在 [安裝程式] 對話方塊中，將相同的選項設定為 [**使用者名稱**]。|  
|PWD|密碼。<br /><br /> 這是選擇性的關鍵字，驅動程式永遠不會將它寫入檔案。 在對密碼安全的 Paradox 檔案進行**SQLDriverConnect**的呼叫時，會使用它。 每當開啟資料表時，所使用的密碼就會是有效的。 如果未在連接字串中傳遞任何密碼，就不會為該資料表建立任何密碼。 如果資料表有不同的密碼，就無法在同一個會話中開啟多個，也無法聯結資料表。|  
|READONLY|TRUE 表示將檔案設為唯讀;FALSE 表示讓檔案不是唯讀的。<br /><br /> 這會在 [安裝程式] 對話方塊中設定與 [**唯讀**] 相同的選項。|  
|串接|要使用之引擎的背景執行緒數目。 這個值為3，而且無法變更。<br /><br /> 這會在 [安裝程式] 對話方塊中設定與**執行緒**相同的選項。|
