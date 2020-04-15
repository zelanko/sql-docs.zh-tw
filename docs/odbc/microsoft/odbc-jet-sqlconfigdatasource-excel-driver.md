---
title: ODBC 噴氣 SQLConfigData 來源(Excel 驅動程式) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], Excel Driver
- Excel driver [ODBC], SqlConfigDataSource
ms.assetid: 885b3bea-f4b6-4902-b994-f78a912b612f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a76482acd1182d900336d7ac9826b16968e00caa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81293008"
---
# <a name="odbc-jet-sqlconfigdatasource-excel-driver"></a>ODBC Jet SQLConfigDataSource (Excel 驅動程式)
> [!NOTE]  
>  本主題提供特定於 Excel 驅動程式的資訊。 有關此功能的一般資訊,請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的相應主題。  
  
 **SQLConfigDataSource**函數用於動態添加、修改或刪除數據源,使用以下關鍵字。  
  
|關鍵字|描述|  
|-------------|-----------------|  
|DBQ|對於存取 Microsoft Excel 5.0 或更高版本檔時的 Microsoft Excel 驅動程式,工作簿檔的名稱。<br /><br /> 這將在設置對話框中設置與**資料庫**相同的選項。|  
|預設 DIR|目錄的路徑規範。<br /><br /> 這將設置與設定對話方塊中的 **「選擇目錄」** 或 **「選擇工作簿」** 相同的選項。|  
|DESCRIPTION|數據源中數據的說明。<br /><br /> 這將設置與設置對話方塊中的 **「說明」** 相同的選項。|  
|DRIVER|驅動程式 DLL 的路徑規範。|  
|驅動程式識別碼|驅動程式的整數 ID。<br /><br /> 534 (微軟 Excel 3.0)<br /><br /> 278 (微軟 Excel 4.0)<br /><br /> 22 (微軟 Excel 5.0/7.0)<br /><br /> 790 (微軟 Excel 97-2003)|  
|FIL|檔案類型,例如 Excel 3.0、Excel 4.0、Excel 5.0、Excel 7.0、Excel 97、Excel 2000 或 Excel 2003。|  
|第一羅哈斯名稱|指示區域第一行的單元格是否包含表 (1) 的列名稱 (0)。|  
|馬克斯坎羅斯|根據現有數據設置列的數據類型時要掃描的行數。<br /><br /> 可以輸入從 1 到 16 的數位來掃描行。 該值預設為 8;如果設置為 0,則掃描所有行。 (超出限制的數位將返回錯誤。<br /><br /> 這將在設置對話框中設置與 **「要掃描的行」** 相同的選項。|  
|READONLY|TRUE 使檔為唯讀;FALSE 使檔不唯讀。<br /><br /> 這將在設置對話框中設置與 **「唯讀」** 相同的選項。|  
|執行緒|發動機要使用的後台線程數。 對於 Microsoft Access 驅動程式,此值預設為 3,但可以更改。 對於 dBASE,MicrosoftExcel 驅動程式此值為 3,不能更改。<br /><br /> 這將設置與設置對話方塊中的 **「線程」** 相同的選項。|
