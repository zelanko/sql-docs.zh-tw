---
description: 安裝程式 DLL 函式摘要
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3666808659abb29a1f5a1eb1e8be62e8cf0507f6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461230"
---
# <a name="installer-dll-function-summary"></a>安裝程式 DLL 函式摘要
下表說明安裝程式 DLL 中的函數。 如需每個函式語法和語義的詳細資訊，請參閱 [安裝程式 DLL API 參考](../../../odbc/reference/syntax/installer-dll-api-reference-function.md)。  
  
|Task|函式名稱|用途|  
|----------|-------------------|-------------|  
|安裝 ODBC|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|載入驅動程式特定的安裝 DLL。|  
||[SQLGetInstalledDrivers](../../../odbc/reference/syntax/sqlgetinstalleddrivers-function.md)|傳回已安裝的驅動程式清單。|  
||[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|將驅動程式新增至系統資訊。|  
||[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|傳回驅動程式管理員的目標目錄。|  
||[SQLInstallerError](../../../odbc/reference/syntax/sqlinstallererror-function.md)|傳回安裝程式函數的錯誤或狀態資訊。|  
||[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|將翻譯工具新增至系統資訊。|  
||[SQLPostInstallerError](../../../odbc/reference/syntax/sqlpostinstallererror-function.md)|允許驅動程式或翻譯工具安裝程式庫回報錯誤。|  
||[SQLRemoveDriver](../../../odbc/reference/syntax/sqlremovedriver-function.md)|從系統資訊中移除驅動程式。|  
||[SQLRemoveDriverManager](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)|從系統資訊移除 ODBC 核心元件。|  
||[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|從系統資訊中移除翻譯工具。|  
|設定資料來源|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|呼叫驅動程式特定的安裝 DLL。|  
||[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|顯示一個對話方塊來加入資料來源。|  
||[SQLGetConfigMode](../../../odbc/reference/syntax/sqlgetconfigmode-function.md)|抓取設定模式，這個模式會指出列出 DSN 值的 Odbc.ini 專案在系統資訊中的位置。|  
||[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|將值寫入系統資訊。|  
||[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|顯示對話方塊以選取翻譯工具。|  
||[SQLManageDataSources](../../../odbc/reference/syntax/sqlmanagedatasources.md)|顯示對話方塊，以設定資料來源和驅動程式。|  
||[SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)|從檔案 Dsn 讀取資訊。|  
||[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|移除預設的資料來源。|  
||[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|移除資料來源。|  
||[SQLSetConfigMode](../../../odbc/reference/syntax/sqlsetconfigmode-function.md)|設定設定模式，指出列出 DSN 值的 Odbc.ini 專案在系統資訊中的位置。|  
||[SQLValidDSN](../../../odbc/reference/syntax/sqlvaliddsn-function.md)|檢查資料來源名稱的長度和有效性。|  
||[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|加入資料來源。|  
||[SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)|將資訊寫入檔案 Dsn。|  
||[SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|取得系統資訊中的值。|
