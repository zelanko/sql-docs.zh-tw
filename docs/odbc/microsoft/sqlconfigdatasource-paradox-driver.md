---
description: SQLConfigDataSource (Paradox 驅動程式)
title: SQLConfigDataSource (Paradox 驅動程式) |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ced7a482f79426961e8532cd343691b3f023703c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411934"
---
# <a name="sqlconfigdatasource-paradox-driver"></a>SQLConfigDataSource (Paradox 驅動程式)
> [!NOTE]  
>  本主題提供 Paradox 驅動程式特定的資訊。 如需此函數的一般資訊，請參閱 [ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的適當主題。  
  
 用來動態加入、修改或刪除資料來源的 **SQLConfigDataSource** 函數會使用下列關鍵字。  
  
|關鍵字|描述|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|欄位的排序次序。<br /><br /> 使用 Paradox 驅動程式時，順序可以是 ASCII (預設) 、國際、瑞典文、芬蘭文或挪威文（丹麥文）。<br /><br /> 這會在 [設定] 對話方塊中，將相同的選項設定為 [ **排序次序** ]。|  
|DBQ|資料庫檔案的名稱。<br /><br /> 這會將相同的選項設定為 [安裝] 對話方塊中的 [ **資料庫** ]。|  
|DEFAULTDIR|目錄的路徑規格。|  
|DESCRIPTION|資料來源中資料的描述。<br /><br /> 這會將相同的選項設定為 [安裝] 對話方塊中的 [ **描述** ]。|  
|DRIVER|驅動程式 DLL 的路徑規格。|  
|DRIVERID|驅動程式的整數識別碼。<br /><br /> 26 (Paradox 3. x) <br /><br /> 282 (Paradox 4. x) <br /><br /> 538 (Paradox 5.x) |  
|獨家|判斷資料庫是否會在獨佔模式中開啟 (一次只有一位使用者存取) 或共用模式， (一次由多位使用者存取) 。 可以是 true (獨佔模式) 或 false (共用模式) 。<br /><br /> 這會將相同的選項設定為 [安裝] 對話方塊中的 [ **獨佔** ]。|  
|FIL|檔案類型 Paradox 3.x、Paradox 4.x 或 Paradox 5。x|  
|FILETYPE|Text 驅動程式的檔案類型 (文字) 。|  
|PAGETIMEOUT|指定一段時間（以十分之一秒為限），頁面 (（如果未使用）) 會在移除之前保留在緩衝區中。 預設值為600十分之一秒 (60 秒) 。 請注意，此選項會套用至所有使用 ODBC 驅動程式的資料來源。<br /><br /> 這會將相同的選項設定為 [設定] 對話方塊中的 **頁面超時** 。|  
|PARADOXNETPATH|包含 Paradox 鎖定資料庫之目錄的完整路徑，因為它包含 PDOXUSRS.net 檔 (的 Paradox 4。*x*) 或 PARADOX.net 檔案 (的 PARADOX 為5。*x*) 。 如果目錄不包含這些檔案的其中一個，Paradox 驅動程式會建立一個。 如需這些檔案的詳細資訊，請參閱 Paradox 檔。<br /><br /> 在可以選取網路目錄之前，必須輸入 Paradox 使用者名稱。<br /><br /> 這會將相同的選項設定為 [安裝] 對話方塊中的 [ **選取網路目錄** ]。|  
|PARADOXNETSTYLE|若為 Paradox 驅動程式，則在存取 Paradox 資料時要使用的網路存取樣式：「3. x」代表 Paradox 3。*x* 或 "4.x" 代表 Paradox 4。*x* 或5。*x*。 如果版本是 Paradox 4，可以設定為 "3.x" 或 "4.x"。*x* 或5。*x*;如果版本為 Paradox 3。*x*，樣式必須是 "3.x"。<br /><br /> 這會將相同的選項設定為 [安裝] 對話方塊中的 [ **Net Style** ]。|  
|PARADOXUSERNAME|如果是 Paradox 驅動程式，則是 Paradox 的使用者名稱。<br /><br /> 這會將相同的選項設定為 [安裝] 對話方塊中的 [ **使用者名稱** ]。|  
|PWD|密碼。<br /><br /> 這是選擇性的關鍵字，且不會由驅動程式寫入檔案。 它是用於對受密碼保護之 Paradox 檔案的 **SQLDriverConnect** 呼叫。 當資料表開啟時，所使用的密碼將會是有效的。 如果連接字串中未傳遞任何密碼，則不會針對該資料表建立任何密碼。 如果資料表具有不同的密碼，就無法在相同的會話中開啟一個以上的資料表，也無法聯結資料表。|  
|READONLY|TRUE 表示將檔案設為唯讀;FALSE 表示讓檔案不是唯讀的。<br /><br /> 這會將相同的選項設定為 [安裝] 對話方塊中的 [ **唯讀** ]。|  
|執行緒|引擎要使用的背景執行緒數目。 此值為3，無法變更。<br /><br /> 這會將相同的選項設定為 [設定] 對話方塊中的 [ **執行緒** ]。|
