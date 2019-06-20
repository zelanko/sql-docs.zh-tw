---
title: SQLConfigDataSource (dBASE Driver) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 63d1951cfe835cbfca23ab366db2216215aa92c3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62665350"
---
# <a name="sqlconfigdatasource-dbase-driver"></a>SQLConfigDataSource (dBASE 驅動程式)
> [!NOTE]  
>  本主題提供 dBASE 驅動程式特定資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 **SQLConfigDataSource**函式，用來新增、 修改或刪除資料來源以動態方式使用下列關鍵字。  
  
|關鍵字|描述|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|欄位會排序順序。<br /><br /> 序列可以是：ASCII （預設值） 或國際。<br /><br /> 這會設定為相同的選項**定序順序**在安裝程式 對話方塊中。|  
|DEFAULTDIR|目錄的路徑規格。|  
|DELETED|DBASE 驅動程式中，指定可以擷取或位於已標示為已刪除的資料列。 如果設為 1，已刪除的資料列不會顯示;如果設為 0，已刪除的資料列會視同未刪除的資料列。<br /><br /> 這會設定為相同的選項**顯示刪除的資料列**在安裝程式 對話方塊中。|  
|DESCRIPTION|資料來源中資料的說明。<br /><br /> 這會設定為相同的選項**描述**在安裝程式 對話方塊中。|  
|DRIVER|驅動程式 DLL 的路徑規格。|  
|DRIVERID|驅動程式的整數識別碼。<br /><br /> 21 (dBASE III)<br /><br /> 277 (dBASE IV)<br /><br /> 533 (dBASE 5.0)|  
|FIL|檔案輸入 dBase III、 dBase IV 或 dBase 5|  
|PAGETIMEOUT|指定的時間，以第二個方法，移除前頁面 （如果未使用） 會保留在緩衝區中的十分之一。 預設值為 600 的十分之一秒 （60 秒）。 請注意，此選項適用於使用 ODBC 驅動程式的所有資料來源。<br /><br /> 這會設定為相同的選項**頁面上的逾時**在安裝程式 對話方塊中。|  
|READONLY|若要使檔案成為唯讀的;，則為 TRUE若要讓檔案不是唯讀，則為 FALSE。<br /><br /> 這會設定為相同的選項**Read Only**在安裝程式 對話方塊中。|  
|STATISTICS|DBASE 驅動程式時，您可以決定是否接近資料表大小統計資料。 請注意，此選項適用於使用 ODBC 驅動程式的所有資料來源。<br /><br /> 這會設定為相同的選項**近似資料列計數**在安裝程式 對話方塊中。|  
|執行緒|引擎使用的背景執行緒數目。 這個值會是 3，而且無法變更。<br /><br /> 這會設定為相同的選項**執行緒**在安裝程式 對話方塊中。|
