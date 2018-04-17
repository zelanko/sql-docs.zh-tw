---
title: SQLConfigDataSource (dBASE 驅動程式) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- DBase driver [ODBC], SQLConfigDataSource
- SQLConfigDataSource function [ODBC], dBASE Driver
ms.assetid: 19909902-054c-4e19-9c06-a212aace13fe
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e18b5fe320c5c46f8c4f148334b0dd5a1e8d54b4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sqlconfigdatasource-dbase-driver"></a>SQLConfigDataSource (dBASE 驅動程式)
> [!NOTE]  
>  本主題提供 dBASE 驅動程式特定資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC 應用程式開發介面參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 **SQLConfigDataSource**函式，用於新增、 修改或刪除資料來源以動態方式使用下列關鍵字。  
  
|關鍵字|Description|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|欄位排序順序。<br /><br /> 序列可以是： ASCII （預設值） 或國際標準。<br /><br /> 這會設定為相同的選項**定序順序**安裝程式 對話方塊中。|  
|DEFAULTDIR|要在目錄的路徑規格。|  
|DELETED |DBASE 驅動程式時，指定可以擷取或位於已標示為已刪除的資料列。 如果設定為 1，已刪除的資料列不會顯示。如果設定為 0，已刪除的資料列會視同未刪除的資料列。<br /><br /> 這會設定為相同的選項**顯示刪除的資料列**安裝程式 對話方塊中。|  
|DESCRIPTION|資料來源中資料的描述。<br /><br /> 這會設定為相同的選項**描述**安裝程式 對話方塊中。|  
|DRIVER|要驅動程式 DLL 的路徑規格。|  
|DRIVERID|驅動程式的整數識別碼。<br /><br /> 21 (dBASE III)<br /><br /> 277 (dBASE IV)<br /><br /> 533 (dBASE 5.0)|  
|FIL|檔案輸入 dBase III，IV，dBase 或 dBase 5|  
|PAGETIMEOUT|指定一段時間中的每秒，被移除之前頁面 （如果不使用） 會保留在緩衝區中的十分之一。 預設值為 600 的十分之一秒 （60 秒）。 請注意，此選項適用於使用 ODBC 驅動程式的所有資料來源。<br /><br /> 這會設定為相同的選項**頁面逾時**安裝程式 對話方塊中。|  
|READONLY|True 表示要使檔案成為唯讀的。若要讓檔案不是唯讀，則為 FALSE。<br /><br /> 這會設定為相同的選項**Read Only**安裝程式 對話方塊中。|  
|STATISTICS|DBASE 驅動程式時，會判斷是否會計算資料表大小的統計資料值。 請注意，此選項適用於使用 ODBC 驅動程式的所有資料來源。<br /><br /> 這會設定為相同的選項**近似資料列計數**安裝程式 對話方塊中。|  
|執行緒|引擎使用的背景執行緒數目。 此值為 3，而且無法變更。<br /><br /> 這會設定為相同的選項**執行緒**安裝程式 對話方塊中。|
