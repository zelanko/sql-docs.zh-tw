---
description: SQLConfigDataSource (Access 驅動程式)
title: SQLConfigDataSource (Access 驅動程式) |Microsoft Docs
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
ms.openlocfilehash: deb777e0d1d4a4e3ea9a45968256ad23dbeb56ab
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411984"
---
# <a name="sqlconfigdatasource-access-driver"></a>SQLConfigDataSource (Access 驅動程式)
> [!NOTE]  
>  本主題提供存取驅動程式特定的資訊。 如需此函數的一般資訊，請參閱 [ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的適當主題。  
  
 用來動態加入、修改或刪除資料來源的 **SQLConfigDataSource** 函數會使用下列關鍵字。  
  
|關鍵字|描述|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|欄位的排序次序。<br /><br /> 這會在 [設定] 對話方塊中，將相同的選項設定為 [ **排序次序** ]。|  
|COMPACT_DB|在資料庫檔案上執行資料壓縮。 的格式如下： COMPACT_DB =<path_name><optionaL_sort_order>\<optional ENCRYPT keyword> 。<br /><br /> 在具有 DSN 關鍵字的相同語句中使用 COMPACT_DB 關鍵字時，此驅動程式會忽略 DSN 關鍵字。 因此，壓縮資料庫並指定 DSN 是兩個步驟的程式。|  
|CREATE_DB|建立資料庫檔案。 的格式如下： CREATE_DB =<path_name>\<optional_sort-order><optional_ENCRYPT 關鍵字>，其中路徑名稱是 Microsoft Access 資料庫的完整路徑。 如果路徑名稱指定了現有的資料庫，就會傳回錯誤。 在 [Microsoft Access 安裝] 對話方塊中按下 [建立] 按鈕時，會在 [新增資料庫] 對話方塊中設定排序次序。 如果未指定排序次序，則會使用一般。<br /><br /> 在具有 DSN 關鍵字的相同語句中使用 CREATE_DB 關鍵字時，此驅動程式會忽略 DSN 關鍵字。 因此，建立資料庫和指定 DSN 是兩個步驟的程式。使用 CREATE_DB 關鍵字時，如果要建立的 Microsoft Access 資料庫的路徑名稱包含一或多個空格，則必須以雙引號括住整個路徑名稱，如下列範例所示：<br /><br /> "C:\PROGRAM FILES\COMMON FILES \ MyAccess .mdb"<br /><br /> "C:\PROGRAM FILES\Access2.mdb"<br /><br /> CREATE_DB = C:\TEMP\test.mdb (不需要引號) |  
|CREATE_SYSDB|建立系統資料庫檔案。 的格式如下： CREATE_SYSDB = \<path-name> \<optional-sort-order> ，其中路徑名稱是 Microsoft Access 資料庫的完整路徑。 如果路徑名稱指定了現有的資料庫，就會傳回錯誤。 在 [ **ODBC Microsoft Access 安裝程式**] 對話方塊中按一下 [**建立**] 按鈕時，會在 [**新增資料庫**] 對話方塊中設定排序次序。 如果未指定排序次序，則會使用一般。|  
|CREATE_V2DB|建立與 Microsoft Access 2.0 相容的資料庫檔案。 的格式如下： CREATE_V2DB = \<path-name> \<optional-sort-order> ，其中路徑名稱是 Microsoft Access 資料庫的完整路徑。 如果路徑名稱指定了現有的資料庫，就會傳回錯誤。 在 [Microsoft Access 安裝] 對話方塊中按下 [建立] 按鈕時，會在 [新增資料庫] 對話方塊中設定排序次序。 如果未指定排序次序，則會使用一般。<br /><br /> 在具有 DSN 關鍵字的相同語句中使用 CREATE_V2DB 關鍵字時，此驅動程式會忽略 DSN 關鍵字。 因此，建立資料庫和指定 DSN 是兩個步驟的程式。<br /><br /> 使用 CREATE_V2DB 關鍵字時，如果要建立的 Microsoft Access 資料庫的路徑名稱包含一或多個空格，則必須以雙引號括住整個路徑名稱，如下列範例所示：<br /><br /> "C:\PROGRAM FILES\COMMON FILES \ MyAccess .mdb"<br /><br /> "C:\PROGRAM FILES\Access2.mdb"<br /><br /> CREATE_V2DB = C:\TEMP\test.mdb (不需要引號) |  
|DBQ|資料庫檔案的名稱。<br /><br /> 這會將相同的選項設定為 [安裝] 對話方塊中的 [ **資料庫** ]。|  
|DEFAULTDIR|資料庫檔案的路徑規格。|  
|DESCRIPTION|資料來源中資料的描述。<br /><br /> 這會將相同的選項設定為 [安裝] 對話方塊中的 [ **描述** ]。|  
|DRIVER|驅動程式 DLL 的路徑規格。|  
|DRIVERID|驅動程式的整數識別碼。  25 (Microsoft Access) |  
|FIL|Microsoft Access 的檔案類型 MS 存取|  
|IMPLICITCOMMITSYNC|判斷 Microsoft Access 驅動程式是否會以非同步方式執行內部或隱含認可。 此值一開始會設定為 "Yes"，這表示 Microsoft Access 驅動程式會等候內部/隱性交易中的認可完成。<br /><br /> 此選項的值不應變更，而不需要仔細考慮結果。 如需有關選項的詳細資訊，請參閱《 *Microsoft Jet 資料庫引擎程式設計人員指南》*。<br /><br /> 這會將相同的選項設定為 [安裝] 對話方塊中的 [ **ImplicitCommitSync** ]。|  
|MAXBUFFERSIZE|以 kb 為單位的內部緩衝區大小（以 kb 為單位），這是 Microsoft Access 用來將資料傳入和傳出磁片的大小。 預設緩衝區大小為 2048 KB (顯示為 2048) 。 可使用256整除的任何整數值。 這會將相同的選項設定為 [安裝] 對話方塊中的 **緩衝區大小** 。|  
|MAXSCANROWS|根據現有資料設定資料行的資料類型時，所要掃描的資料列數目。<br /><br /> 您可以輸入從1到16的數位來掃描資料列。 值預設為 8;如果設定為0，則會掃描所有資料列。  (超出限制的數位將會傳回錯誤。 ) <br /><br /> 這會將相同的選項設定為要在 [設定] 對話方塊中掃描的資料 **列** 。|  
|PAGETIMEOUT|以毫秒為單位，指定頁面 (（如果未使用）) 在被移除之前保留在緩衝區中的時間長度（以毫秒為單位）。 預設值是 (0.5 秒) 的五到十分之一秒。 請注意，此選項會套用至所有使用 ODBC 驅動程式的資料來源。<br /><br /> 這會將相同的選項設定為 [設定] 對話方塊中的 **頁面超時** 。|  
|PWD|密碼。|  
|READONLY|TRUE 表示將檔案設為唯讀;FALSE 表示讓檔案不是唯讀的。<br /><br /> 這會將相同的選項設定為 [安裝] 對話方塊中的 [ **唯讀** ]。|  
|REPAIR_DB|修復在認可程式期間發生的失敗而損毀的資料庫。<br /><br /> 在具有 DSN 關鍵字的相同語句中使用 REPAIR_DB 關鍵字時，此驅動程式會忽略 DSN 關鍵字。 因此，修復資料庫並指定 DSN 是兩個步驟的程式。|  
|SYSTEMDB|若為 Microsoft Access 驅動程式，則為系統資料庫檔案的路徑規格。<br /><br /> 這會將相同的選項設定為 [安裝] 對話方塊中的 [ **系統資料庫** ]。|  
|執行緒|引擎要使用的背景執行緒數目。 此值預設為3，但可以變更。<br /><br /> 這會將相同的選項設定為 [設定] 對話方塊中的 [ **執行緒** ]。|  
|UID|若為 Microsoft Access 驅動程式，則為用於登入的使用者識別碼名稱。|  
|USERCOMMITSYNC|判斷 Microsoft Access 驅動程式是否會以非同步方式執行使用者定義的交易。 此值最初會設定為 "Yes"，這表示 Microsoft Access 驅動程式會等候使用者定義交易中的認可完成。<br /><br /> 此選項的值不應變更，而不需要仔細考慮結果。 如需有關選項的詳細資訊，請參閱《 *Microsoft Jet 資料庫引擎程式設計人員指南》*。<br /><br /> 這會將相同的選項設定為 [安裝] 對話方塊中的 [ **UserCommitSync** ]。|
