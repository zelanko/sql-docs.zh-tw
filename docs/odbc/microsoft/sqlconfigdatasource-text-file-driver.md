---
title: SQLConfigData 源(文字檔案驅動程式) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], SQLConfigDataSource
- SQLConfigDataSource function [ODBC], Text File Driver
ms.assetid: c505d36e-1e72-47b2-a9e5-e4926b408468
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2d2809f9b15dd6843e4404c7cf1887c3caa015a3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283918"
---
# <a name="sqlconfigdatasource-text-file-driver"></a>SQLConfigDataSource (文字檔驅動程式)
> [!NOTE]  
>  本主題提供特定於文本檔驅動程序的資訊。 有關此功能的一般資訊,請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的相應主題。  
  
 **SQLConfigDataSource**函數用於動態添加、修改或刪除數據源,使用以下關鍵字。  
  
|關鍵字|描述|  
|-------------|-----------------|  
|字元集|對於文本驅動程式、OEM 或 ANSI。|  
|科爾納梅頭|對於 Text 驅動程式,指示第一個資料記錄是否將指定列名稱。 真或假。|  
|預設 DIR|目錄的路徑規範。|  
|DESCRIPTION|數據源中數據的說明。<br /><br /> 這將設置與設置對話方塊中的 **「說明」** 相同的選項。|  
|DRIVER|驅動程式 DLL 的路徑規範。|  
|驅動程式識別碼|驅動程式的整數 ID。 27 (text)|  
|延伸|列出資料來源上文字檔的檔案名副檔名。<br /><br /> 這將在設置對話框中設置與**擴展清單**相同的選項。|  
|FIL|檔案類型 文字|  
|檔案類型|文字驅動程式(文字)的檔案類型。|  
|FORMAT|對於文本驅動程式,可以是固定長度、TABDE限制、CSVDE限制(通過逗號)或 DELIMITED(通過括弧中指定的特殊字元)。 特殊字元的長度是一個字元,可以是字元、十進位或十六進位格式。|  
|馬克斯坎羅斯|根據現有數據設置列的數據類型時要掃描的行數。<br /><br /> 對於 Text 驅動程式,您可以輸入從 1 到 32767 的數位,以便掃描的行數;但是,該值將始終預設為 25。 (超出限制的數位將返回錯誤。<br /><br /> 這將在設置對話框中設置與 **「要掃描的行」** 相同的選項。|  
|READONLY|TRUE 使檔為唯讀;FALSE 使檔不唯讀。<br /><br /> 這將在設置對話框中設置與 **「唯讀」** 相同的選項。|
