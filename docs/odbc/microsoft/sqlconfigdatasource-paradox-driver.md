---
title: SQLConfig數據源(悖論驅動程式) |微軟文件
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
ms.openlocfilehash: 68e60d7ca9c37865c1b265297d24591638a44965
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283928"
---
# <a name="sqlconfigdatasource-paradox-driver"></a>SQLConfigDataSource (Paradox 驅動程式)
> [!NOTE]  
>  本主題提供特定於悖論驅動程序的資訊。 有關此功能的一般資訊,請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的相應主題。  
  
 **SQLConfigDataSource**函數用於動態添加、修改或刪除數據源,使用以下關鍵字。  
  
|關鍵字|描述|  
|-------------|-----------------|  
|整理順序|欄位排序的順序。<br /><br /> 使用 Paradox 驅動程式時,序列可以是 ASCII(預設)、國際、瑞典-芬蘭或挪威-丹麥。<br /><br /> 這將設置與設定對話框中 **「整理序列」** 相同的選項。|  
|DBQ|資料庫檔案的名稱。<br /><br /> 這將在設置對話框中設置與**資料庫**相同的選項。|  
|預設 DIR|目錄的路徑規範。|  
|DESCRIPTION|數據源中數據的說明。<br /><br /> 這將設置與設置對話方塊中的 **「說明」** 相同的選項。|  
|DRIVER|驅動程式 DLL 的路徑規範。|  
|驅動程式識別碼|驅動程式的整數 ID。<br /><br /> 26 (悖論 3.x)<br /><br /> 282 (悖論 4.x)<br /><br /> 538 (悖論 5.x)|  
|獨家|確定資料庫將以獨佔模式打開(一次只由一個用戶訪問)還是共用模式(一次由多個用戶訪問)。 可以是 true(獨佔模式)或 false(共用模式)。<br /><br /> 這將在設置對話框中設置與 **「獨佔」** 相同的選項。|  
|FIL|檔案類型悖論 3.x、悖論 4.x 或悖論 5.x|  
|檔案類型|文字驅動程式(文字)的檔案類型。|  
|頁面逾時|指定頁面(如果不使用)在刪除之前保留在緩衝區中的時間段(以十分之一秒表示)。 默認值為 600 秒(60 秒)。 請注意,此選項適用於使用 ODBC 驅動程式的所有資料來源。<br /><br /> 這將在設置對話框中設置與**頁面超時**相同的選項。|  
|已悖論網路路徑|包含 Paradox 鎖資料庫的目錄的完整路徑,因為它包含PDOXUSRS.net檔(在悖論 4 中)。*x*) 或PARADOX.net檔(在悖論 5 中)。*x*)。 如果目錄不包含這些檔之一,則 Paradox 驅動程式將創建一個。 有關這些文件的資訊,請參閱 Paradox 文檔。<br /><br /> 在選擇網路目錄之前,必須輸入 Paradox 使用者名。<br /><br /> 這將在設置對話框中設置與**選擇網路目錄**相同的選項。|  
|悖論網路風格|對於悖論驅動程式,在訪問悖論數據時要使用的網路訪問樣式:對於悖論 3 的「3.x」。。*x*或"4.x"表示悖論 4。*x*或 5。*x*. . 如果版本為悖論 4,則可以設置為"3.x"或"4.x"。*x*或 5。*x;* 如果版本是悖論 3。*x*,樣式必須為"3.x"。<br /><br /> 這將在設定對話框中設置與 **「網路樣式」** 相同的選項。|  
|悖論|對於悖論驅動程式,悖論使用者名。<br /><br /> 這將在設置對話框中設置與**使用者名**相同的選項。|  
|PWD|密碼。<br /><br /> 這是一個可選的關鍵字,驅動程式永遠不會寫入檔。 它用於針對密碼安全的悖論檔的調用**SQLDriverConnect。** 每當打開表時,使用的密碼將有效。 如果在連接字串中未傳遞密碼,則未為該表建立密碼。 如果表具有不同的密碼,則無法在同一會話中打開多個密碼,也無法聯接表。|  
|READONLY|TRUE 使檔為唯讀;FALSE 使檔不唯讀。<br /><br /> 這將在設置對話框中設置與 **「唯讀」** 相同的選項。|  
|執行緒|發動機要使用的後台線程數。 此值為 3,無法更改。<br /><br /> 這將設置與設置對話方塊中的 **「線程」** 相同的選項。|
