---
title: SQLConfigDataSource （文字檔驅動程式） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], SQLConfigDataSource
- SQLConfigDataSource function [ODBC], Text File Driver
ms.assetid: c505d36e-1e72-47b2-a9e5-e4926b408468
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2d2809f9b15dd6843e4404c7cf1887c3caa015a3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81283918"
---
# <a name="sqlconfigdatasource-text-file-driver"></a>SQLConfigDataSource (文字檔驅動程式)
> [!NOTE]  
>  本主題提供文字檔驅動程式特定的資訊。 如需此函數的一般資訊，請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)底下的適當主題。  
  
 用來以動態方式加入、修改或刪除資料來源的**SQLConfigDataSource**函數會使用下列關鍵字。  
  
|關鍵字|描述|  
|-------------|-----------------|  
|CHARACTERSET|針對文字驅動程式，OEM 或 ANSI。|  
|COLNAMEHEADER|若為文字驅動程式，表示資料的第一筆記錄是否會指定資料行名稱。 TRUE 或 FALSE。|  
|DEFAULTDIR|目錄的路徑規格。|  
|DESCRIPTION|資料來源中的資料描述。<br /><br /> 這會在 [安裝程式] 對話方塊中設定與 [**描述**] 相同的選項。|  
|DRIVER|驅動程式 DLL 的路徑規格。|  
|DRIVERID|驅動程式的整數識別碼。 27（文字）|  
|延伸模組|列出資料來源上的文字檔副檔名。<br /><br /> 這會在 [安裝程式] 對話方塊中設定與 [**延伸模組清單**] 相同的選項。|  
|FIL|檔案類型文字|  
|類型|文字驅動程式的檔案類型（文字）。|  
|FORMAT|對於文字驅動程式，可以是 FIXEDLENGTH、TABDELIMITED、CSVDELIMITED （逗號）或分隔（）（依據括弧中指定的特殊字元）。 特殊字元是長度的一個字元，而且可以是字元、十進位或十六進位格式。|  
|MAXSCANROWS|根據現有的資料來設定資料行的資料類型時，所要掃描的資料列數目。<br /><br /> 針對文字驅動程式，您可以輸入從1到32767的數位，以進行要掃描的資料列數目;不過，此值一律會預設為25。 （超出限制的數位將會傳回錯誤）。<br /><br /> 這會在 [安裝程式] 對話方塊中，設定與**要掃描**的資料列相同的選項。|  
|READONLY|TRUE 表示將檔案設為唯讀;FALSE 表示讓檔案不是唯讀的。<br /><br /> 這會在 [安裝程式] 對話方塊中設定與 [**唯讀**] 相同的選項。|
