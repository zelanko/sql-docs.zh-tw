---
title: SQLConfig資料來源(dBASE 驅動程式) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DBase driver [ODBC], SQLConfigDataSource
- SQLConfigDataSource function [ODBC], dBASE Driver
ms.assetid: 19909902-054c-4e19-9c06-a212aace13fe
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 18c6721b4f34772e8c3cd8e4f515233f80566fb3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283968"
---
# <a name="sqlconfigdatasource-dbase-driver"></a>SQLConfigDataSource (dBASE 驅動程式)
> [!NOTE]  
>  本主題提供特定於 dBASE 驅動程式的資訊。 有關此功能的一般資訊,請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的相應主題。  
  
 **SQLConfigDataSource**函數用於動態添加、修改或刪除數據源,使用以下關鍵字。  
  
|關鍵字|描述|  
|-------------|-----------------|  
|整理順序|欄位排序的順序。<br /><br /> 序列可以是:ASCII(預設值)或國際。<br /><br /> 這將設置與設定對話框中 **「整理序列」** 相同的選項。|  
|預設 DIR|目錄的路徑規範。|  
|DELETED |對於 dBASE 驅動程式,指定是否可以檢索或定位標記為已刪除的行。 如果設置為 1,則不顯示已刪除的行;如果設置為 1,則不顯示已刪除的行。如果設置為 0,則刪除的行將被視為與未刪除的行相同。<br /><br /> 這將設定與設定對話框中**顯示已刪除的行**相同的選項。|  
|DESCRIPTION|數據源中數據的說明。<br /><br /> 這將設置與設置對話方塊中的 **「說明」** 相同的選項。|  
|DRIVER|驅動程式 DLL 的路徑規範。|  
|驅動程式識別碼|驅動程式的整數 ID。<br /><br /> 21 (dBASE III)<br /><br /> 277 (dBASE IV)<br /><br /> 533 (dBASE 5.0)|  
|FIL|檔案類型 dBase III、dBase IV 或 dBase 5|  
|頁面逾時|指定頁面(如果不使用)在刪除之前保留在緩衝區中的時間段(以十分之一秒表示)。 默認值為 600 秒(60 秒)。 請注意,此選項適用於使用 ODBC 驅動程式的所有資料來源。<br /><br /> 這將在設置對話框中設置與**頁面超時**相同的選項。|  
|READONLY|TRUE 使檔為唯讀;FALSE 使檔不唯讀。<br /><br /> 這將在設置對話框中設置與 **「唯讀」** 相同的選項。|  
|STATISTICS|對於 dBASE 驅動程式,確定表大小統計資訊是否近似。 請注意,此選項適用於使用 ODBC 驅動程式的所有資料來源。<br /><br /> 這將在設置對話框中設置與 **「近似行計數」** 相同的選項。|  
|執行緒|發動機要使用的後台線程數。 此值為 3,無法更改。<br /><br /> 這將設置與設置對話方塊中的 **「線程」** 相同的選項。|
