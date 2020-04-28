---
title: SQLConfigDataSource （dBASE 驅動程式） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DBase driver [ODBC], SQLConfigDataSource
- SQLConfigDataSource function [ODBC], dBASE Driver
ms.assetid: 19909902-054c-4e19-9c06-a212aace13fe
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 18c6721b4f34772e8c3cd8e4f515233f80566fb3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81283968"
---
# <a name="sqlconfigdatasource-dbase-driver"></a>SQLConfigDataSource (dBASE 驅動程式)
> [!NOTE]  
>  本主題提供 dBASE 驅動程式特定的資訊。 如需此函數的一般資訊，請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)底下的適當主題。  
  
 用來以動態方式加入、修改或刪除資料來源的**SQLConfigDataSource**函數會使用下列關鍵字。  
  
|關鍵字|描述|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|排序欄位的順序。<br /><br /> 順序可以是： ASCII （預設值）或國際。<br /><br /> 這會在 [安裝程式] 對話方塊中，將相同的選項設定為 [**排序次序**]。|  
|DEFAULTDIR|目錄的路徑規格。|  
|DELETED |對於 dBASE 驅動程式，指定是否可以抓取或定位已標示為已刪除的資料列。 如果設定為1，就不會顯示已刪除的資料列;如果設定為0，刪除的資料列就會被視為與非刪除的資料列相同。<br /><br /> 這會設定與 [設定] 對話方塊中 [**顯示已刪除**的資料列] 相同的選項。|  
|DESCRIPTION|資料來源中的資料描述。<br /><br /> 這會在 [安裝程式] 對話方塊中設定與 [**描述**] 相同的選項。|  
|DRIVER|驅動程式 DLL 的路徑規格。|  
|DRIVERID|驅動程式的整數識別碼。<br /><br /> 21（dBASE III）<br /><br /> 277（dBASE IV）<br /><br /> 533（dBASE 5.0）|  
|FIL|檔案類型 dBase III、dBase IV 或 dBase 5|  
|PAGETIMEOUT|指定在移除之前，頁面（如果未使用）會保留在緩衝區中的一段時間，以十分之一秒為限。 預設值為600十分之一秒（60秒）。 請注意，此選項適用于使用 ODBC 驅動程式的所有資料來源。<br /><br /> 這會設定與 [設定] 對話方塊中**頁面超時**相同的選項。|  
|READONLY|TRUE 表示將檔案設為唯讀;FALSE 表示讓檔案不是唯讀的。<br /><br /> 這會在 [安裝程式] 對話方塊中設定與 [**唯讀**] 相同的選項。|  
|STATISTICS|針對 dBASE 驅動程式，判斷資料表大小統計資料是否近似。 請注意，此選項適用于使用 ODBC 驅動程式的所有資料來源。<br /><br /> 這會設定與 [設定] 對話方塊中的 [**近似資料列計數**] 相同的選項。|  
|串接|要使用之引擎的背景執行緒數目。 這個值為3，且無法變更。<br /><br /> 這會在 [安裝程式] 對話方塊中設定與**執行緒**相同的選項。|
