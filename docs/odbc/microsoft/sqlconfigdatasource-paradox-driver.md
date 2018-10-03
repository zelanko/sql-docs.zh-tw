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
manager: craigg
ms.openlocfilehash: ad9c944af33da86e0d4f85769288f4ab7b6c369f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47694588"
---
# <a name="sqlconfigdatasource-paradox-driver"></a>SQLConfigDataSource (Paradox 驅動程式)
> [!NOTE]  
>  本主題提供 Paradox 驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 **SQLConfigDataSource**函式，用來新增、 修改或刪除資料來源以動態方式使用下列關鍵字。  
  
|關鍵字|描述|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|欄位會排序順序。<br /><br /> 使用 Paradox 驅動程式時，序列可以是 ASCII （預設值）、 國際、 瑞典文-芬蘭文或挪威文-丹麥文。<br /><br /> 這會設定為相同的選項**定序順序**在安裝程式 對話方塊中。|  
|DBQ|資料庫檔案的名稱。<br /><br /> 這會設定為相同的選項**資料庫**在安裝程式 對話方塊中。|  
|DEFAULTDIR|目錄的路徑規格。|  
|DESCRIPTION|資料來源中資料的說明。<br /><br /> 這會設定為相同的選項**描述**在安裝程式 對話方塊中。|  
|DRIVER|驅動程式 DLL 的路徑規格。|  
|DRIVERID|驅動程式的整數識別碼。<br /><br /> 26 (paradox 3.x)<br /><br /> 282 (paradox 4.x)<br /><br /> 538 (paradox 5.x)|  
|獨佔|判斷資料庫是否將會開啟以獨佔模式 （存取只有一位使用者一次），或共用 （存取多個使用者一次） 的模式。 可以是 true （獨佔模式） 或 false （共用模式）。<br /><br /> 這會設定為相同的選項**獨佔**在安裝程式 對話方塊中。|  
|FIL|檔案類型 Paradox 3.x，Paradox 4.x 或 Paradox 5.x|  
|檔案類型|文字驅動程式 （文字） 的檔案類型。|  
|PAGETIMEOUT|指定的時間，以第二個方法，移除前頁面 （如果未使用） 會保留在緩衝區中的十分之一。 預設值為 600 的十分之一秒 （60 秒）。 請注意，此選項適用於使用 ODBC 驅動程式的所有資料來源。<br /><br /> 這會設定為相同的選項**頁面上的逾時**在安裝程式 對話方塊中。|  
|PARADOXNETPATH|包含 Paradox 鎖定資料庫，因為它包含 PDOXUSRS.net 檔案的目錄的完整路徑 (Paradox 4。*x*) 或 PARADOX.net 檔案 (Paradox 5。*x*)。 如果目錄不包含其中一個檔案，Paradox 驅動程式會建立一個。 如需這些檔案的詳細資訊，請參閱 Paradox 文件。<br /><br /> 可以選取網路目錄之前，必須輸入 Paradox 使用者名稱。<br /><br /> 這會設定為相同的選項**選取 [網路目錄**在安裝程式] 對話方塊中。|  
|PARADOXNETSTYLE|Paradox 驅動程式，網路存取存取 Paradox 資料時要使用的樣式： 其中一個 「 3.x"Paradox 3。*x*或 「 4.x"Paradox 4 for。*x*或 5。*x*。 可以設定為"3.x"或"4.x"Paradox 4 版本時。*x*或 5。*x*; 如果版本為 Paradox 3。*x*，樣式必須是"3.x"。<br /><br /> 這會設定為相同的選項**Net 樣式**在安裝程式 對話方塊中。|  
|PARADOXUSERNAME|Paradox 驅動程式中，按一下 Paradox 使用者名稱。<br /><br /> 這會設定為相同的選項**使用者名**在安裝程式 對話方塊中。|  
|PWD|密碼。<br /><br /> 這是一個選擇性的關鍵字，並將永遠不會寫入至檔案驅動程式。 它會在呼叫**SQLDriverConnect**針對受密碼保護 Paradox 檔案。 每當開啟資料表時，才有效用的密碼。 如果連接字串中傳遞沒有密碼，則該資料表建立沒有密碼。 如果資料表有不同的密碼，多個無法開啟相同的工作階段中，也不聯結的資料表。|  
|READONLY|若要使檔案成為唯讀的;，則為 TRUE若要讓檔案不是唯讀，則為 FALSE。<br /><br /> 這會設定為相同的選項**Read Only**在安裝程式 對話方塊中。|  
|執行緒|引擎使用的背景執行緒數目。 此值為 3，並無法變更。<br /><br /> 這會設定為相同的選項**執行緒**在安裝程式 對話方塊中。|
