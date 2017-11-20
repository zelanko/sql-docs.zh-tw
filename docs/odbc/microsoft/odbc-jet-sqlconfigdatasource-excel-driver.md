---
title: "ODBC Jet SQLConfigDataSource （Excel 驅動程式） |Microsoft 文件"
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
- SQLConfigDataSource function [ODBC], Excel Driver
- Excel driver [ODBC], SqlConfigDataSource
ms.assetid: 885b3bea-f4b6-4902-b994-f78a912b612f
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9a4d5d0b2feb0a09aafeb441c6b33260e4f0738b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="odbc-jet-sqlconfigdatasource-excel-driver"></a>ODBC Jet SQLConfigDataSource （Excel 驅動程式）
> [!NOTE]  
>  本主題提供 Excel 驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC 應用程式開發介面參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 **SQLConfigDataSource**函式，用於新增、 修改或刪除資料來源以動態方式使用下列關鍵字。  
  
|關鍵字|Description|  
|-------------|-----------------|  
|DBQ|Microsoft Excel 驅動程式時存取 Microsoft Excel 5.0 或更新版本的檔案，活頁簿檔案的名稱。<br /><br /> 這會設定為相同的選項**資料庫**安裝程式 對話方塊中。|  
|DEFAULTDIR|要在目錄的路徑規格。<br /><br /> 這會設定為相同的選項**選取目錄**或**選取活頁簿**安裝程式 對話方塊中。|  
|DESCRIPTION|資料來源中資料的描述。<br /><br /> 這會設定為相同的選項**描述**安裝程式 對話方塊中。|  
|DRIVER|要驅動程式 DLL 的路徑規格。|  
|DRIVERID|驅動程式的整數識別碼。<br /><br /> 534 (Microsoft Excel 3.0)<br /><br /> 278 (Microsoft Excel 4.0)<br /><br /> 22 (Microsoft Excel 5.0/7.0)<br /><br /> 790 (Microsoft Excel 97-2003)|  
|FIL|檔案類型，例如，Excel 3.0、 Excel 4.0、 Excel 5.0、 Excel 7.0、 Excel 97、 Excel 2000 或 Excel 2003。|  
|FIRSTROWHASNAMES|表示範圍的第一列儲存格是否包含資料表 (1) 的資料行名稱，或不 (0)。|  
|於 MAXSCANROWS|設定現有的資料為基礎的資料行的資料類型時，要掃描的資料列數目。<br /><br /> 您可以輸入 1 到 16 的數字，要掃描的資料列。 預設值為 8。如果設定為 0，會掃描所有資料列。 （限制以外的數字會傳回錯誤）。<br /><br /> 這會設定為相同的選項**要掃描的資料列**安裝程式 對話方塊中。|  
|READONLY|True 表示要使檔案成為唯讀的。若要讓檔案不是唯讀，則為 FALSE。<br /><br /> 這會設定為相同的選項**Read Only**安裝程式 對話方塊中。|  
|執行緒|引擎使用的背景執行緒數目。 Microsoft Access 驅動程式，這個值會預設為 3，但可以變更。 如 dBASE MicrosoftExceldriver 此值為 3，且無法變更。<br /><br /> 這會設定為相同的選項**執行緒**安裝程式 對話方塊中。|

