---
title: SQLConfigDataSource （Access 驅動程式） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 85b515ed4c30d68e62a49e1044c4ddf6f5cc5ab1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67985231"
---
# <a name="sqlconfigdatasource-access-driver"></a>SQLConfigDataSource (Access 驅動程式)
> [!NOTE]  
>  本主題提供存取驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 **SQLConfigDataSource**函式，用來新增、 修改或刪除資料來源以動態方式使用下列關鍵字。  
  
|關鍵字|描述|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|欄位會排序順序。<br /><br /> 這會設定為相同的選項**定序順序**在安裝程式 對話方塊中。|  
|COMPACT_DB|資料庫檔案上執行資料壓縮。 具有下列格式：COMPACT_DB = < path_name >< optionaL_sort_order >\<選擇性的加密關鍵字 >。<br /><br /> 當使用 COMPACT_DB 關鍵字使用 DSN 關鍵字相同的陳述式中，此驅動程式會忽略 DSN 關鍵字。 因此，壓縮的資料庫，並指定 DSN 是兩步驟程序。|  
|CREATE_DB|建立資料庫檔案。 具有下列格式：CREATE_DB = < path_name >\<optional_sort 順序 >< optional_ENCRYPT 關鍵字 >，其中的路徑名稱是 Microsoft Access 資料庫的完整路徑。 如果路徑名稱指定現有的資料庫，則會傳回錯誤。 排序次序會在新的資料庫 對話方塊，顯示在 Microsoft 存取設定 對話方塊中按下 建立 按鈕時，設定會啟動。 如果未不指定任何排序順序，則會使用一般。<br /><br /> 當使用 CREATE_DB 關鍵字使用 DSN 關鍵字相同的陳述式中，此驅動程式會忽略 DSN 關鍵字。 因此，建立資料庫，並指定 DSN 是兩步驟程序。當使用 CREATE_DB 關鍵字，如果要建立 Microsoft Access 資料庫的路徑名稱包含一或多個空格，然後整個路徑名稱必須括以雙引號括住，如下列範例所示：<br /><br /> "C:\PROGRAM FILES\COMMON FILES\ MyAccess.mdb"<br /><br /> "C:\PROGRAM FILES\Access2.mdb"<br /><br /> CREATE_DB=C:\TEMP\test.mdb （沒有引號所需）|  
|CREATE_SYSDB|建立系統資料庫檔案。 具有下列格式：CREATE_SYSDB =\<路徑名稱 >\<選擇性排序次序 >，其中的路徑名稱是 Microsoft Access 資料庫的完整路徑。 如果路徑名稱指定現有的資料庫，則會傳回錯誤。 排序次序就會設定為啟動中**新的資料庫**對話方塊顯示時**建立**，就會引發**ODBC Microsoft Access 安裝**對話方塊。 如果未不指定任何排序順序，則會使用一般。|  
|CREATE_V2DB|建立與 Microsoft Access 2.0 相容的資料庫檔案。 具有下列格式：CREATE_V2DB =\<路徑名稱 >\<選擇性排序次序 >，其中的路徑名稱是 Microsoft Access 資料庫的完整路徑。 如果路徑名稱指定現有的資料庫，則會傳回錯誤。 排序次序會在新的資料庫 對話方塊，顯示在 Microsoft 存取設定 對話方塊中按下 建立 按鈕時，設定會啟動。 如果未不指定任何排序順序，則會使用一般。<br /><br /> 當使用 CREATE_V2DB 關鍵字使用 DSN 關鍵字相同的陳述式中，此驅動程式會忽略 DSN 關鍵字。 因此，建立資料庫，並指定 DSN 是兩步驟程序。<br /><br /> 當使用 CREATE_V2DB 關鍵字，如果要建立 Microsoft Access 資料庫的路徑名稱包含一或多個空格，然後整個路徑名稱必須括以雙引號括住，如下列範例所示：<br /><br /> "C:\PROGRAM FILES\COMMON FILES\ MyAccess.mdb"<br /><br /> "C:\PROGRAM FILES\Access2.mdb"<br /><br /> CREATE_V2DB=C:\TEMP\test.mdb （沒有引號所需）|  
|DBQ|資料庫檔案的名稱。<br /><br /> 這會設定為相同的選項**資料庫**在安裝程式 對話方塊中。|  
|DEFAULTDIR|資料庫檔案的路徑規格。|  
|DESCRIPTION|資料來源中資料的說明。<br /><br /> 這會設定為相同的選項**描述**在安裝程式 對話方塊中。|  
|DRIVER|驅動程式 DLL 的路徑規格。|  
|DRIVERID|驅動程式的整數識別碼。  25 (Microsoft Access)|  
|FIL|檔案類型為 Microsoft Access 的 MS Access|  
|IMPLICITCOMMITSYNC|判斷是否 Microsoft Access 驅動程式會執行內部或隱含認可以非同步的方式。 此值一開始是設定為 [是]，這表示 Microsoft Access 驅動程式會等待完成內部/隱含交易中認可。<br /><br /> 此選項的值不應該變更而不需要仔細考量的後果。 如需有關選項的詳細資訊，請參閱 < *Microsoft Jet Database Engine 程式設計人員指南*。<br /><br /> 這會設定為相同的選項**ImplicitCommitSync**在安裝程式 對話方塊中。|  
|MAXBUFFERSIZE|內部緩衝區大小，以 kb 為單位，Microsoft Access 所用來傳輸資料進出磁碟。 預設緩衝區大小為 2048 KB （顯示為 2048年）。 可以使用任何以 256 整除的整數值。 這會設定為相同的選項**緩衝區大小**在安裝程式 對話方塊中。|  
|於 MAXSCANROWS|若要設定現有的資料為基礎的資料行的資料類型時，要掃描的資料列數目。<br /><br /> 要掃描的資料列，您可以輸入 1 到 16 的數字。 預設值為 8。如果它設定為 0，則會掃描所有資料列。 （限制以外的數字會傳回錯誤）。<br /><br /> 這會設定為相同的選項**要掃描的資料列**在安裝程式 對話方塊中。|  
|PAGETIMEOUT|指定的時間週期，以毫秒為單位，移除前頁面 （如果未使用） 會保留在緩衝區中。 預設值是五個-十分之一秒 （0.5 秒為單位）。 請注意，此選項適用於使用 ODBC 驅動程式的所有資料來源。<br /><br /> 這會設定為相同的選項**頁面上的逾時**在安裝程式 對話方塊中。|  
|PWD|密碼。|  
|READONLY|若要使檔案成為唯讀的;，則為 TRUE若要讓檔案不是唯讀，則為 FALSE。<br /><br /> 這會設定為相同的選項**Read Only**在安裝程式 對話方塊中。|  
|REPAIR_DB|修復損毀所認可程序中發生的失敗的資料庫。<br /><br /> 當使用 REPAIR_DB 關鍵字使用 DSN 關鍵字相同的陳述式中，此驅動程式會忽略 DSN 關鍵字。 因此，修復資料庫，並指定 DSN 是兩步驟程序。|  
|SYSTEMDB|Microsoft Access 驅動程式中，按一下 系統資料庫檔案的路徑規格。<br /><br /> 這會設定為相同的選項**系統資料庫**在安裝程式 對話方塊中。|  
|執行緒|引擎使用的背景執行緒數目。 這個值預設為 3，但可以變更。<br /><br /> 這會設定為相同的選項**執行緒**在安裝程式 對話方塊中。|  
|UID|Microsoft Access 驅動程式的使用者 ID 名稱會用來登入。|  
|USERCOMMITSYNC|判斷是否 Microsoft Access 驅動程式會執行使用者定義的交易以非同步的方式。 此值一開始是設定為 [是]，這表示 Microsoft Access 驅動程式將等候中的使用者定義的交易完成認可。<br /><br /> 此選項的值不應該變更而不需要仔細考量的後果。 如需有關選項的詳細資訊，請參閱 < *Microsoft Jet Database Engine 程式設計人員指南*。<br /><br /> 這會設定為相同的選項**UserCommitSync**在安裝程式 對話方塊中。|
