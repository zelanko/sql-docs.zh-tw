---
description: SQLConfigDataSource (dBASE 驅動程式)
title: SQLConfigDataSource (dBASE 驅動程式) |Microsoft Docs
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
ms.openlocfilehash: 23e734c5aafc903e210eea18f002f4c5e8d7a456
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411954"
---
# <a name="sqlconfigdatasource-dbase-driver"></a>SQLConfigDataSource (dBASE 驅動程式)
> [!NOTE]  
>  本主題提供 dBASE 驅動程式特定的資訊。 如需此函數的一般資訊，請參閱 [ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的適當主題。  
  
 用來動態加入、修改或刪除資料來源的 **SQLConfigDataSource** 函數會使用下列關鍵字。  
  
|關鍵字|描述|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|欄位的排序次序。<br /><br /> 順序可以是： ASCII (預設) 或國際。<br /><br /> 這會在 [設定] 對話方塊中，將相同的選項設定為 [ **排序次序** ]。|  
|DEFAULTDIR|目錄的路徑規格。|  
|DELETED|針對 dBASE 驅動程式，指定是否可以取出或定位已標示為已刪除的資料列。 如果設定為1，則不會顯示已刪除的資料列;如果設定為0，則會將已刪除的資料列視為與未刪除的資料列相同。<br /><br /> 這會將相同的選項設定為在 [設定] 對話方塊中 **顯示 [已刪除** 的資料列]。|  
|DESCRIPTION|資料來源中資料的描述。<br /><br /> 這會將相同的選項設定為 [安裝] 對話方塊中的 [ **描述** ]。|  
|DRIVER|驅動程式 DLL 的路徑規格。|  
|DRIVERID|驅動程式的整數識別碼。<br /><br /> 21 (dBASE III) <br /><br /> 277 (dBASE IV) <br /><br /> 533 (dBASE 5.0) |  
|FIL|檔案類型 dBase III、dBase IV 或 dBase 5|  
|PAGETIMEOUT|指定一段時間（以十分之一秒為限），頁面 (（如果未使用）) 會在移除之前保留在緩衝區中。 預設值為600十分之一秒 (60 秒) 。 請注意，此選項會套用至所有使用 ODBC 驅動程式的資料來源。<br /><br /> 這會將相同的選項設定為 [設定] 對話方塊中的 **頁面超時** 。|  
|READONLY|TRUE 表示將檔案設為唯讀;FALSE 表示讓檔案不是唯讀的。<br /><br /> 這會將相同的選項設定為 [安裝] 對話方塊中的 [ **唯讀** ]。|  
|STATISTICS|針對 dBASE 驅動程式，判斷資料表大小統計資料是否為近似值。 請注意，此選項會套用至所有使用 ODBC 驅動程式的資料來源。<br /><br /> 這會將相同的選項設定為 [設定] 對話方塊中的 **近似資料列計數** 。|  
|執行緒|引擎要使用的背景執行緒數目。 此值為3，無法變更。<br /><br /> 這會將相同的選項設定為 [設定] 對話方塊中的 [ **執行緒** ]。|
