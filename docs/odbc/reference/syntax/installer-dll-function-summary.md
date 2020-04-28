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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ddaf20334a84833433961a49e17724d354945c5a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298768"
---
# <a name="installer-dll-function-summary"></a>安裝程式 DLL 函式摘要
下表描述安裝程式 DLL 中的函數。 如需每個函式之語法和語義的詳細資訊，請參閱[安裝程式 DLL API 參考](../../../odbc/reference/syntax/installer-dll-api-reference-function.md)。  
  
|工作|函式名稱|目的|  
|----------|-------------------|-------------|  
|安裝 ODBC|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|載入驅動程式特定的安裝程式 DLL。|  
||[SQLGetInstalledDrivers](../../../odbc/reference/syntax/sqlgetinstalleddrivers-function.md)|傳回已安裝之驅動程式的清單。|  
||[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|將驅動程式新增至系統資訊。|  
||[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|傳回驅動程式管理員的目標目錄。|  
||[SQLInstallerError](../../../odbc/reference/syntax/sqlinstallererror-function.md)|傳回安裝程式函式的錯誤或狀態資訊。|  
||[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|將翻譯工具加入至系統資訊。|  
||[SQLPostInstallerError](../../../odbc/reference/syntax/sqlpostinstallererror-function.md)|允許驅動程式或轉譯器安裝程式庫報告錯誤。|  
||[SQLRemoveDriver](../../../odbc/reference/syntax/sqlremovedriver-function.md)|從系統資訊移除驅動程式。|  
||[SQLRemoveDriverManager](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)|從系統資訊移除 ODBC core 元件。|  
||[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|從系統資訊移除翻譯工具。|  
|設定資料來源|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|呼叫驅動程式特定的安裝程式 DLL。|  
||[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|顯示對話方塊，以加入資料來源。|  
||[SQLGetConfigMode](../../../odbc/reference/syntax/sqlgetconfigmode-function.md)|抓取設定模式，指出在系統資訊中列出 DSN 值的 Odbc 專案所在的位置。|  
||[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|將值寫入系統資訊。|  
||[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|顯示用來選取翻譯工具的對話方塊。|  
||[SQLManageDataSources](../../../odbc/reference/syntax/sqlmanagedatasources.md)|顯示對話方塊，以設定資料來源和驅動程式。|  
||[SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)|從檔案 Dsn 讀取資訊。|  
||[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|移除預設的資料來源。|  
||[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|移除資料來源。|  
||[SQLSetConfigMode](../../../odbc/reference/syntax/sqlsetconfigmode-function.md)|設定表示在系統資訊中列出 DSN 值之 Odbc 專案所在位置的設定模式。|  
||[SQLValidDSN](../../../odbc/reference/syntax/sqlvaliddsn-function.md)|檢查資料來源名稱的長度和有效性。|  
||[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|加入資料來源。|  
||[SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)|將資訊寫入檔案 Dsn。|  
||[SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|從系統資訊取得值。|
