---
title: 安裝程式 DLL 功能摘要 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298768"
---
# <a name="installer-dll-function-summary"></a>安裝程式 DLL 函式摘要
下表描述了安裝程式 DLL 中的函數。 有關每個函數的語法和語義的詳細資訊,請參閱[安裝程式 DLL API 參考](../../../odbc/reference/syntax/installer-dll-api-reference-function.md)。  
  
|Task|函式名稱|目的|  
|----------|-------------------|-------------|  
|安裝 ODBC|[SQL 設定驅動程式](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|載入特定於驅動程式的安裝程式 DLL。|  
||[SQLGet 安裝驅動程式](../../../odbc/reference/syntax/sqlgetinstalleddrivers-function.md)|返回已安裝驅動程式的清單。|  
||[SQL安裝驅動程式Ex](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|向系統資訊添加驅動程式。|  
||[SQLInstall 驅動程式管理員](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|返回驅動程式管理員的目標目錄。|  
||[SQL 安裝程式錯誤](../../../odbc/reference/syntax/sqlinstallererror-function.md)|返回安裝程式函數的錯誤或狀態資訊。|  
||[SQL安裝翻譯器Ex](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|向系統資訊添加轉換器。|  
||[SQLPost安裝程式錯誤](../../../odbc/reference/syntax/sqlpostinstallererror-function.md)|允許驅動程式或轉換器設置庫報告錯誤。|  
||[SQL 移除驅動程式](../../../odbc/reference/syntax/sqlremovedriver-function.md)|從系統資訊中移除驅動程式。|  
||[SQL 移除驅動程式管理員](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)|從系統資訊中刪除 ODBC 核心元件。|  
||[SQL 刪除轉換器](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|從系統資訊中刪除轉換器。|  
|設定資料來源|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|呼叫特定於驅動程式的安裝程式 DLL。|  
||[SQLCreate資料來源](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|顯示一個對話框以添加數據源。|  
||[SQLGet 設定模式](../../../odbc/reference/syntax/sqlgetconfigmode-function.md)|檢索指示 Odbc.ini 條目列表 DSN 值在系統資訊中的位置的配置模式。|  
||[SQLGet 私人設定檔字串](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|向系統資訊寫入值。|  
||[SQLGet 轉換器](../../../odbc/reference/syntax/sqlgettranslator-function.md)|顯示要選擇譯員的對話方塊。|  
||[SQLManageDataSources](../../../odbc/reference/syntax/sqlmanagedatasources.md)|顯示用於配置數據源和驅動程序的對話方塊。|  
||[SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)|從檔 DSN 讀取資訊。|  
||[SQL 移除預設資料來源](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|刪除預設資料來源。|  
||[SQLRemoveDSNfromini](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|刪除數據源。|  
||[SQLSet 設定模式](../../../odbc/reference/syntax/sqlsetconfigmode-function.md)|設置配置模式,指示 Odbc.ini 條目列表 DSN 值在系統資訊中的位置。|  
||[SQLValidDSN](../../../odbc/reference/syntax/sqlvaliddsn-function.md)|檢查數據源名稱的長度和有效性。|  
||[SQLwriteSntoini](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|添加數據源。|  
||[SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)|將資訊寫入檔 DSN。|  
||[SQLWrite 私有設定檔字串](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|從系統資訊獲取值。|
