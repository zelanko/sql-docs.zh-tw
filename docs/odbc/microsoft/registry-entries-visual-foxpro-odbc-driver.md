---
title: 登錄項目 (Visual FoxPro ODBC Driver) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: de287802693adb18e39509fdc0e7577d05984949
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63316831"
---
# <a name="registry-entries-visual-foxpro-odbc-driver"></a>登錄項目 (Visual FoxPro ODBC Driver)
當您安裝 Visual FoxPro ODBC Driver 時，安裝程式會更新您的系統登錄中，登錄機碼 HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCInst.ini，以新增新的金鑰，稱為 Microsoft Visual FoxPro 驅動程式中。 在該機碼，如下表所示的值會加入。  
  
|值名稱|值類型|值|  
|----------------|----------------|-----------|  
|APILevel|REG_SZ|"1"|  
|ConnectFunctions|REG_SZ|「 YYN"|  
|驅動程式|REG_SZ|Vfpodbc.dll 檔案系統路徑|  
|DriverODBCVer|REG_SZ|"02.50"|  
|FileExtns|REG_SZ|"*.dbf,\*.cdx,\*.fpt"|  
|FileUsage|REG_SZ|"1"|  
|安裝程式|REG_SZ|Vfpodbc.dll 檔案系統路徑|  
|SQLLevel|REG_SZ|"0"|  
  
 安裝程式也會將 「 Visual FoxPro 檔案 」，表示預設的 Visual FoxPro 驅動程式，您的系統 HKEY_CURRENT_USER\SOFTWARE\ODBC\Odbc.ini 索引鍵的索引鍵。 此機碼，安裝程式會將下表中所述的值。  
  
|值名稱|值類型|值|  
|----------------|----------------|-----------|  
|驅動程式|REG_SZ|Vfpodbc.dll 檔案系統路徑|  
  
 您將 Visual FoxPro ODBC 資料來源新增至您的 ODBC 設定，每次新的索引鍵被加入針對該資料來源名稱。 資料來源的值對應至您在設定的值**ODBC Visual FoxPro 設定**對話方塊中，如下表所示。  
  
|值名稱 （關鍵字）|值類型|值|  
|----------------------------|----------------|-----------|  
|自動分頁|REG_SQ|任何支援的定序順序|  
|描述|REG_SZ|資料來源的使用者說明|  
|驅動程式||Vfpodbc.dll 檔案系統路徑|  
|排除||[是] 或 [否]|  
|BackgroundFetch||[是] 或 [否]|  
|SourceDB|REG_SZ|路徑。雙位元組字元的檔案|  
|SourceType|REG_SZ|「 雙位元組字元"或者"DBF"|  
  
 您不應該直接; 存取這項資訊登錄的任何系統管理會處理由 ODBC 管理員，當您新增、 修改或刪除資料來源。  
  
 您可以使用其中一些關鍵字和值中的參數[SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md) ODBC API 函式。
