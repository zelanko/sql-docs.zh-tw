---
title: SQLConfigDataSource （Paradox 驅動程式） |Microsoft 文件
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
- SQLConfigDataSource function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLConfigDataSource
ms.assetid: 59e84c4e-debe-49d7-b97b-84c736b0c793
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b308748a351617808ca74863c681e562a9df74a6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32904203"
---
# <a name="sqlconfigdatasource-paradox-driver"></a>SQLConfigDataSource （Paradox 驅動程式）
> [!NOTE]  
>  本主題提供 Paradox 驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC 應用程式開發介面參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 **SQLConfigDataSource**函式，用於新增、 修改或刪除資料來源以動態方式使用下列關鍵字。  
  
|關鍵字|Description|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|欄位排序順序。<br /><br /> 序列使用 Paradox 驅動程式時，可以是 ASCII （預設值）、 國際、 瑞典文-芬蘭文或挪威文丹麥文。<br /><br /> 這會設定為相同的選項**定序順序**安裝程式 對話方塊中。|  
|DBQ|資料庫檔案的名稱。<br /><br /> 這會設定為相同的選項**資料庫**安裝程式 對話方塊中。|  
|DEFAULTDIR|要在目錄的路徑規格。|  
|DESCRIPTION|資料來源中資料的描述。<br /><br /> 這會設定為相同的選項**描述**安裝程式 對話方塊中。|  
|DRIVER|要驅動程式 DLL 的路徑規格。|  
|DRIVERID|驅動程式的整數識別碼。<br /><br /> 26 (paradox 3.x)<br /><br /> 282 (paradox 4.x)<br /><br /> 538 (paradox 5.x)|  
|獨佔|判斷資料庫將會開啟以獨佔模式 （由只有一位使用者一次存取） 或共用模式 （由多個使用者每次存取）。 可以是 （獨佔模式） 為 true 或 false （共用模式）。<br /><br /> 這會設定為相同的選項**獨佔**安裝程式 對話方塊中。|  
|FIL|檔案類型 Paradox 3.x，Paradox 4.x 或 Paradox 5.x|  
|檔案類型|文字驅動程式 （文字） 的檔案類型。|  
|PAGETIMEOUT|指定一段時間中的每秒，被移除之前頁面 （如果不使用） 會保留在緩衝區中的十分之一。 預設值為 600 的十分之一秒 （60 秒）。 請注意，此選項適用於使用 ODBC 驅動程式的所有資料來源。<br /><br /> 這會設定為相同的選項**頁面逾時**安裝程式 對話方塊中。|  
|PARADOXNETPATH|包含 Paradox 鎖定資料庫，因為它包含 PDOXUSRS.net 檔案的目錄的完整路徑 (在 Paradox 4。*x*) 或 PARADOX.net 檔案 (Paradox 5。*x*)。 如果目錄不包含這些檔案，Paradox 驅動程式會建立一個。 如需這些檔案的資訊，請參閱 Paradox 文件。<br /><br /> 可以選取網路目錄之前，必須輸入 Paradox 使用者名稱。<br /><br /> 這會設定為相同的選項**選取網路目錄**安裝程式 對話方塊中。|  
|PARADOXNETSTYLE|Paradox 驅動程式時，網路存取所存取 Paradox 資料時要使用的樣式： Paradox 3 任一"3.x"。*x*或 「 4.x 」 的 Paradox 4。*x*或 5。*x*。 可以設定 「 3.x"或"4.x"Paradox 4 版本時。*x*或 5。*x*; 如果版本是 Paradox 3。*x*，樣式必須是"3.x"。<br /><br /> 這會設定為相同的選項**Net 樣式**安裝程式 對話方塊中。|  
|PARADOXUSERNAME|Paradox 驅動程式中，按一下 Paradox 使用者名稱。<br /><br /> 這會設定為相同的選項**使用者名**安裝程式 對話方塊中。|  
|PWD|密碼。<br /><br /> 這是一個選擇性的關鍵字，而且永遠不會將寫入至檔案的驅動程式。 用於呼叫**SQLDriverConnect**針對受密碼保護 Paradox 檔案。 每當開啟資料表時，才有效用的密碼。 如果連接字串中傳遞沒有密碼，則該資料表建立沒有密碼。 如果資料表具有不同的密碼，在相同的工作階段中，無法開啟多個也聯結的資料表。|  
|READONLY|True 表示要使檔案成為唯讀的。若要讓檔案不是唯讀，則為 FALSE。<br /><br /> 這會設定為相同的選項**Read Only**安裝程式 對話方塊中。|  
|執行緒|引擎使用的背景執行緒數目。 此值為 3，並無法變更。<br /><br /> 這會設定為相同的選項**執行緒**安裝程式 對話方塊中。|
