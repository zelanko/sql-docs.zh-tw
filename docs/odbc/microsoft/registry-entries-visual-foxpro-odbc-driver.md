---
title: "登錄項目 （Visual FoxPro ODBC 驅動程式） |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- registry keys [ODBC]
- Visual FoxPro ODBC driver [ODBC], registry entries
- keys [ODBC]
- FoxPro ODBC driver [ODBC], registry entries
ms.assetid: 1a63d92d-ca3a-46ae-911f-6788292c801e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6a975ff73eb4b2ef48af05ccfdf595ae9c3233f0
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="registry-entries-visual-foxpro-odbc-driver"></a>登錄項目 （Visual FoxPro ODBC 驅動程式）
當您安裝 Visual FoxPro ODBC 驅動程式時，安裝程式會更新您的系統登錄中，登錄機碼 HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCInst.ini，若要加入新的金鑰，呼叫 Microsoft Visual FoxPro 驅動程式中。 下該機碼，會使用下表中描述的值。  
  
|值名稱|值類型|值|  
|----------------|----------------|-----------|  
|APILevel|REG_SZ|"1"|  
|ConnectFunctions|REG_SZ|「 YYN"|  
|驅動程式|REG_SZ|Vfpodbc.dll 檔案系統路徑|  
|DriverODBCVer|REG_SZ|"02.50"|  
|FileExtns|REG_SZ|「 *.dbf，\*.cdx，\*.fpt"|  
|FileUsage|REG_SZ|"1"|  
|安裝程式|REG_SZ|Vfpodbc.dll 檔案系統路徑|  
|SQLLevel|REG_SZ|"0"|  
  
 安裝程式也會加入 「 Visual FoxPro 檔案 」，表示預設 Visual FoxPro 驅動程式時，您的系統 HKEY_CURRENT_USER\SOFTWARE\ODBC\Odbc.ini 索引鍵的索引鍵。 此機碼，安裝程式會將下表中描述的值。  
  
|值名稱|值類型|值|  
|----------------|----------------|-----------|  
|驅動程式|REG_SZ|Vfpodbc.dll 檔案系統路徑|  
  
 Visual FoxPro ODBC 資料來源加入您的 ODBC 組態，每當新的金鑰就會加入該資料來源名稱。 資料來源的值對應於您在設定的值**ODBC Visual FoxPro 安裝**對話方塊，如同下表所列。  
  
|值名稱 （關鍵字）|值類型|值|  
|----------------------------|----------------|-----------|  
|自動分頁|REG_SQ|任何支援的定序順序|  
|Description|REG_SZ|使用者資料來源的描述|  
|驅動程式||Vfpodbc.dll 檔案系統路徑|  
|排除||[是] 或 [否]|  
|BackgroundFetch||[是] 或 [否]|  
|SourceDB|REG_SZ|路徑。雙位元組字元的檔案|  
|SourceType|REG_SZ|「 雙位元組字元"或者"DBF"|  
  
 您不應該直接; 存取這項資訊新增、 修改或刪除資料來源時，任何系統管理登錄處理由 ODBC 系統管理員。  
  
 您可以使用這些關鍵字與值的某些中當做參數[SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md) ODBC API 函式。

