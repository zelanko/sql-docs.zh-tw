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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 46bb00fb01ed3fee8098420794af089f2d8b981e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68054080"
---
# <a name="sqlconfigdatasource-text-file-driver"></a>SQLConfigDataSource (文字檔驅動程式)
> [!NOTE]  
>  本主題提供文字檔驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 **SQLConfigDataSource**函式，用來新增、 修改或刪除資料來源以動態方式使用下列關鍵字。  
  
|關鍵字|描述|  
|-------------|-----------------|  
|CHARACTERSET|針對文字驅動程式時，OEM 或 ANSI。|  
|COLNAMEHEADER|文字驅動程式時，表示資料的第一筆記錄是否將指定的資料行名稱。 TRUE 或 FALSE。|  
|DEFAULTDIR|目錄的路徑規格。|  
|DESCRIPTION|資料來源中資料的說明。<br /><br /> 這會設定為相同的選項**描述**在安裝程式 對話方塊中。|  
|DRIVER|驅動程式 DLL 的路徑規格。|  
|DRIVERID|驅動程式的整數識別碼。 27 （文字）|  
|延伸模組|列出資料來源上的文字檔案的副檔名。<br /><br /> 這會設定為相同的選項**延伸模組清單**在安裝程式 對話方塊中。|  
|FIL|檔案類型的文字|  
|檔案類型|文字驅動程式 （文字） 的檔案類型。|  
|FORMAT|文字驅動程式，可以是 FIXEDLENGTH、 TABDELIMITED、 CSVDELIMITED （以逗號分隔） 或 DELIMITED() （藉由指定括號括住的特殊字元）。 特殊字元是一個字元的長度，而且可以是字元、 十進位、 十六進位或十進位格式。|  
|於 MAXSCANROWS|若要設定現有的資料為基礎的資料行的資料類型時，要掃描的資料列數目。<br /><br /> 文字驅動程式，您可以輸入的數字 1 到 32767 之間的掃描; 的資料列數目不過，此值永遠都會預設為 25。 （限制以外的數字會傳回錯誤）。<br /><br /> 這會設定為相同的選項**要掃描的資料列**在安裝程式 對話方塊中。|  
|READONLY|若要使檔案成為唯讀的;，則為 TRUE若要讓檔案不是唯讀，則為 FALSE。<br /><br /> 這會設定為相同的選項**Read Only**在安裝程式 對話方塊中。|
