---
title: "SQLConfigDataSource （文字檔案驅動程式） |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- text file driver [ODBC], SQLConfigDataSource
- SQLConfigDataSource function [ODBC], Text File Driver
ms.assetid: c505d36e-1e72-47b2-a9e5-e4926b408468
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e781871cc8507d10617e1a147fa6d5a7c06ac756
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlconfigdatasource-text-file-driver"></a>SQLConfigDataSource （文字檔案驅動程式）
> [!NOTE]  
>  本主題提供文字檔驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC 應用程式開發介面參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 **SQLConfigDataSource**函式，用於新增、 修改或刪除資料來源以動態方式使用下列關鍵字。  
  
|關鍵字|Description|  
|-------------|-----------------|  
|CHARACTERSET|文字驅動程式、 OEM 或 ANSI。|  
|COLNAMEHEADER|文字驅動程式，則表示資料的第一筆記錄是否將指定的資料行名稱。 TRUE 或 FALSE。|  
|DEFAULTDIR|要在目錄的路徑規格。|  
|DESCRIPTION|資料來源中資料的描述。<br /><br /> 這會設定為相同的選項**描述**安裝程式 對話方塊中。|  
|DRIVER|要驅動程式 DLL 的路徑規格。|  
|DRIVERID|驅動程式的整數識別碼。 27 （文字）|  
|擴充功能|列出的資料來源上的文字檔案的副檔名。<br /><br /> 這會設定為相同的選項**擴充功能清單**安裝程式 對話方塊中。|  
|FIL|檔案類型的文字|  
|檔案類型|文字驅動程式 （文字） 的檔案類型。|  
|FORMAT|文字驅動程式，可以是 FIXEDLENGTH、 TABDELIMITED、 CSVDELIMITED （以逗號分隔） 或 DELIMITED() （藉由指定的括號中的特殊字元）。 特殊字元是一個字元的長度，而且可以是字元、 十進位或十六進位格式。|  
|於 MAXSCANROWS|設定現有的資料為基礎的資料行的資料類型時，要掃描的資料列數目。<br /><br /> 文字驅動程式，您可以輸入的數字 1 到 32767 之間的掃描; 的資料列數目不過，值一律會預設為 25。 （限制以外的數字會傳回錯誤）。<br /><br /> 這會設定為相同的選項**要掃描的資料列**安裝程式 對話方塊中。|  
|READONLY|True 表示要使檔案成為唯讀的。若要讓檔案不是唯讀，則為 FALSE。<br /><br /> 這會設定為相同的選項**Read Only**安裝程式 對話方塊中。|

