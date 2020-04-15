---
title: SQL 設定資料來源(存取驅動程式) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], Access Driver
- Access driver [ODBC], SQLConfigDataSource
ms.assetid: 1b152fb7-fa12-46b9-b168-006bb1355e77
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 48668525b578845fc330881d7c7de503d69d0928
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284048"
---
# <a name="sqlconfigdatasource-access-driver"></a>SQLConfigDataSource (Access 驅動程式)
> [!NOTE]  
>  本主題提供特定於訪問驅動程序的資訊。 有關此功能的一般資訊,請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的相應主題。  
  
 **SQLConfigDataSource**函數用於動態添加、修改或刪除數據源,使用以下關鍵字。  
  
|關鍵字|描述|  
|-------------|-----------------|  
|整理順序|欄位排序的順序。<br /><br /> 這將設置與設定對話框中 **「整理序列」** 相同的選項。|  
|COMPACT_DB|對資料庫檔執行數據壓縮。 具有以下格式:COMPACT_DB*<path_name><optionaL_sort_order>\<可選的 ENCRYPT 關鍵字>。<br /><br /> 當將 COMPACT_DB 關鍵字使用相同的語句與 DSN 關鍵字時,此驅動程式將忽略 DSN 關鍵字。 因此,壓縮資料庫和指定 DSN 是一個兩步過程。|  
|CREATE_DB|創建資料庫檔。 具有以下格式:CREATE_DB* \<<>optional_sort順序><optional_ENCRYPT關鍵字>>path_name,其中路徑名稱是 Microsoft Access 資料庫的完整路徑。 如果路徑名稱指定現有資料庫,則將返回錯誤。 排序順序將與在 Microsoft 訪問設置對話方塊中按下" 按鈕時顯示的「新建資料庫」 對話框中設置。 如果未指定排序順序,則使用"常規"。<br /><br /> 當將CREATE_DB關鍵字使用相同的語句與 DSN 關鍵字時,此驅動程式將忽略 DSN 關鍵字。 因此,創建資料庫並指定 DSN 是一個兩步過程。使用 CREATE_DB 關鍵字時,如果要建立的 Microsoft Access 資料庫的路徑名稱包含一個或多個空格,則整個路徑名稱必須用雙引括起來,如以下範例所示:<br /><br /> "C:程式檔_共用檔]MyAccess.mdb"<br /><br /> "C:_程式檔\訪問2.mdb"<br /><br /> CREATE_DB_C:\TEMP_test.mdb(無需引號)|  
|CREATE_SYSDB|建立系統資料庫檔。 具有以下格式:CREATE_SYSDB=\<路徑名稱>\<可選排序順序>,其中路徑名稱是 Microsoft Access 資料庫的完整路徑。 如果路徑名稱指定現有資料庫,則將返回錯誤。 排序順序將如在**ODBC 微軟存取設定**對話框中按一下 **「創建**」按鈕時顯示的「**新建資料庫**」 對話框中設定。 如果未指定排序順序,則使用"常規"。|  
|CREATE_V2DB|創建與 Microsoft Access 2.0 相容的資料庫檔。 具有以下格式:CREATE_V2DB=\<路徑名稱>\<可選排序順序>,其中路徑名稱是 Microsoft Access 資料庫的完整路徑。 如果路徑名稱指定現有資料庫,則將返回錯誤。 排序順序將與在 Microsoft 訪問設置對話方塊中按下" 按鈕時顯示的「新建資料庫」 對話框中設置。 如果未指定排序順序,則使用"常規"。<br /><br /> 當將CREATE_V2DB關鍵字使用相同的語句與 DSN 關鍵字時,此驅動程式將忽略 DSN 關鍵字。 因此,創建資料庫並指定 DSN 是一個兩步過程。<br /><br /> 使用CREATE_V2DB關鍵字時,如果要建立的 Microsoft Access 資料庫的路徑名稱包含一個或多個空格,則整個路徑名稱必須用雙引括起來,如以下範例所示:<br /><br /> "C:程式檔_共用檔]MyAccess.mdb"<br /><br /> "C:_程式檔\訪問2.mdb"<br /><br /> CREATE_V2DB_C:\TEMP_test.mdb(無需引號)|  
|DBQ|資料庫檔案的名稱。<br /><br /> 這將在設置對話框中設置與**資料庫**相同的選項。|  
|預設 DIR|資料庫文件的路徑規範。|  
|DESCRIPTION|數據源中數據的說明。<br /><br /> 這將設置與設置對話方塊中的 **「說明」** 相同的選項。|  
|DRIVER|驅動程式 DLL 的路徑規範。|  
|驅動程式識別碼|驅動程式的整數 ID。  25 (微軟存取)|  
|FIL|檔案類型 MS 存取微軟存取|  
|隱含提交同步|確定 Microsoft Access 驅動程式將非同步執行內部或隱式提交。 此值最初設置為"是",這意味著 Microsoft Access 驅動程式將等待內部/隱式事務中的提交完成。<br /><br /> 如果不仔細考慮後果,不應改變這一備選辦法的價值。 有關該選項的詳細資訊,請參閱 Microsoft*噴氣資料庫引擎程式師指南*。<br /><br /> 這將在設定對話框中設置與 **「隱式提交同步」** 相同的選項。|  
|最大緩衝大小|Microsoft Access 用於將數據傳輸到磁碟和從磁碟傳輸的內部緩衝區(以千位元組為單位)的大小。 默認緩衝區大小為 2048 KB(顯示為 2048)。 可以使用任何被 256 整數整數值可分割。 這將在設置對話框中設置與**緩衝區大小**相同的選項。|  
|馬克斯坎羅斯|根據現有數據設置列的數據類型時要掃描的行數。<br /><br /> 可以輸入從 1 到 16 的數位來掃描行。 該值預設為 8;如果設置為 0,則掃描所有行。 (超出限制的數位將返回錯誤。<br /><br /> 這將在設置對話框中設置與 **「要掃描的行」** 相同的選項。|  
|頁面逾時|指定頁面(如果不使用)在刪除之前保留在緩衝區中的時間段(以毫秒為單位)。 默認值為五十分之一秒(0.5 秒)。 請注意,此選項適用於使用 ODBC 驅動程式的所有資料來源。<br /><br /> 這將在設置對話框中設置與**頁面超時**相同的選項。|  
|PWD|密碼。|  
|READONLY|TRUE 使檔為唯讀;FALSE 使檔不唯讀。<br /><br /> 這將在設置對話框中設置與 **「唯讀」** 相同的選項。|  
|REPAIR_DB|修復因提交過程中發生的故障而損壞的資料庫。<br /><br /> 當將 REPAIR_DB 關鍵字使用相同的關鍵字與 DSN 關鍵字一起使用時,此驅動程式將忽略 DSN 關鍵字。 因此,修復資料庫和指定 DSN 是一個兩步過程。|  
|系統DB|對於 Microsoft Access 驅動程式,系統資料庫檔的路徑規範。<br /><br /> 這將在設置對話框中設置與**系統資料庫**相同的選項。|  
|執行緒|發動機要使用的後台線程數。 此值預設為 3,但可以更改。<br /><br /> 這將設置與設置對話方塊中的 **「線程」** 相同的選項。|  
|UID|對於 Microsoft Access 驅動程式,用於登錄的使用者 ID 名稱。|  
|使用者提交同步|確定 Microsoft Access 驅動程式是否會非同步執行使用者定義的事務。 此值最初設置為"是",這意味著 Microsoft Access 驅動程式將等待使用者定義的事務中的提交完成。<br /><br /> 如果不仔細考慮後果,不應改變這一備選辦法的價值。 有關該選項的詳細資訊,請參閱 Microsoft*噴氣資料庫引擎程式師指南*。<br /><br /> 這將在設置對話框中設置與**使用者提交同步**相同的選項。|
