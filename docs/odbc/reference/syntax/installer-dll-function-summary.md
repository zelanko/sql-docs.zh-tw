---
title: 安裝程式 DLL 函式摘要 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], installer DLL functions
- installer DLL [ODBC]
ms.assetid: 666c09d3-1e10-4d89-9b42-eda2957a87f0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ecb486f51caa97c715d54885c34575a60bfdfb83
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47723326"
---
# <a name="installer-dll-function-summary"></a>安裝程式 DLL 函式摘要
下表描述在安裝程式 DLL 函式。 如需語法和語意，每個函式的詳細資訊，請參閱[安裝程式 DLL API 參考](../../../odbc/reference/syntax/installer-dll-api-reference-function.md)。  
  
|工作|函數名稱|目的|  
|----------|-------------------|-------------|  
|安裝 ODBC|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|載入特定驅動程式安裝程式 DLL。|  
||[SQLGetInstalledDrivers](../../../odbc/reference/syntax/sqlgetinstalleddrivers-function.md)|傳回一份已安裝的驅動程式。|  
||[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|將驅動程式新增至 系統資訊。|  
||[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|驅動程式管理員會傳回目標目錄。|  
||[SQLInstallerError](../../../odbc/reference/syntax/sqlinstallererror-function.md)|傳回的安裝程式函式的錯誤或狀態資訊。|  
||[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|將轉譯器加入至 系統資訊。|  
||[SQLPostInstallerError](../../../odbc/reference/syntax/sqlpostinstallererror-function.md)|可讓驅動程式或轉譯器安裝程式庫來報告錯誤。|  
||[SQLRemoveDriver](../../../odbc/reference/syntax/sqlremovedriver-function.md)|移除系統資訊中的驅動程式。|  
||[SQLRemoveDriverManager](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)|移除 ODBC 核心元件從 系統資訊。|  
||[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|轉譯器會移除系統資訊。|  
|設定資料來源|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|呼叫特定驅動程式安裝程式 DLL。|  
||[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|顯示對話方塊以加入資料來源。|  
||[SQLGetConfigMode](../../../odbc/reference/syntax/sqlgetconfigmode-function.md)|擷取表示列出資料來源名稱值的 Odbc.ini 項目中的系統資訊的組態模式。|  
||[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|您可以將值寫入系統資訊。|  
||[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|顯示對話方塊以選取轉譯器。|  
||[SQLManageDataSources](../../../odbc/reference/syntax/sqlmanagedatasources.md)|顯示對話方塊以設定資料來源及驅動程式。|  
||[SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)|讀取檔案名稱 （dsn） 中的資訊。|  
||[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|移除預設資料來源。|  
||[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|移除資料來源。|  
||[SQLSetConfigMode](../../../odbc/reference/syntax/sqlsetconfigmode-function.md)|設定指出列出資料來源名稱值的 Odbc.ini 項目中的系統資訊的組態模式。|  
||[SQLValidDSN](../../../odbc/reference/syntax/sqlvaliddsn-function.md)|會檢查長度和有效的資料來源的名稱。|  
||[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|新增資料來源。|  
||[SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)|將資訊寫入至檔案名稱 （dsn）。|  
||[SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|取得值，從 系統資訊。|
