---
title: 註冊表條目(可視化福克斯Pro ODBC驅動程式) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- registry keys [ODBC]
- Visual FoxPro ODBC driver [ODBC], registry entries
- keys [ODBC]
- FoxPro ODBC driver [ODBC], registry entries
ms.assetid: 1a63d92d-ca3a-46ae-911f-6788292c801e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bd2d419a94c45a872789e095b014159b41d7c217
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304835"
---
# <a name="registry-entries-visual-foxpro-odbc-driver"></a>登錄項目 (Visual FoxPro ODBC Driver)
安裝 Visual FoxPro ODBC 驅動程式時,安裝程式在註冊表HKEY_LOCAL_MACHINE_SOFTWARE_ODBC_ODBCInst.ini 中更新系統的註冊表,以添加新金鑰,稱為 Microsoft Visual FoxPro 驅動程式。 在該鍵下,將添加下表中描述的值。  
  
|值名稱|值類型|值|  
|----------------|----------------|-----------|  
|API 等級|REG_SZ|「1」|  
|連線功能|REG_SZ|"YYN"|  
|驅動程式|REG_SZ|vfpodbc.dll 檔案的系統路徑|  
|DriverODBCVer|REG_SZ|"02.50"|  
|檔案 Extns|REG_SZ|".dbf,\*.cdx,\*.fpt"|  
|檔案使用|REG_SZ|「1」|  
|安裝程式|REG_SZ|vfpodbc.dll 檔案的系統路徑|  
|SQLLevel|REG_SZ|"0"|  
  
 安裝程式還將代表預設 Visual FoxPro 驅動程式的密鑰「Visual FoxPro 檔案」添加到系統的HKEY_CURRENT_USER_SOFTWARE_ODBC_Odbc.ini 密鑰。 在此鍵下,安裝程式將添加下表中描述的值。  
  
|值名稱|值類型|值|  
|----------------|----------------|-----------|  
|驅動程式|REG_SZ|vfpodbc.dll 檔案的系統路徑|  
  
 每次將 Visual FoxPro ODBC 資料來源加入 ODBC 設定時,都會為該資料來源名稱添加新密鑰。 數據源的值對應於您在**ODBC Visual FoxPro 安裝程式**對話方塊中設置的值,如下表中列出的。  
  
|值名稱(關鍵字)|值類型|值|  
|----------------------------|----------------|-----------|  
|自動分頁|REG_SQ|任何支援的整理序列|  
|描述|REG_SZ|資料來源的使用者描述|  
|驅動程式||vfpodbc.dll 檔案的系統路徑|  
|獨佔||[是] 或 [否]|  
|背景擷取||[是] 或 [否]|  
|SourceDB|REG_SZ|到的路徑。DBC 檔案|  
|SourceType|REG_SZ|"DBC"或"DBF"|  
  
 您不應直接存取此資訊;因此,您不應直接存取此資訊。當您添加、修改或刪除數據源時,註冊的任何管理將由 ODBC 管理員處理。  
  
 您可以在[SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md) ODBC API 函數中將其中一些關鍵字和值用作參數。
