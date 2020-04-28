---
title: ODBC Jet SQLConfigDataSource （Excel 驅動程式） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], Excel Driver
- Excel driver [ODBC], SqlConfigDataSource
ms.assetid: 885b3bea-f4b6-4902-b994-f78a912b612f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a76482acd1182d900336d7ac9826b16968e00caa
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81293008"
---
# <a name="odbc-jet-sqlconfigdatasource-excel-driver"></a>ODBC Jet SQLConfigDataSource (Excel 驅動程式)
> [!NOTE]  
>  本主題提供 Excel 驅動程式特有的資訊。 如需此函數的一般資訊，請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)底下的適當主題。  
  
 用來以動態方式加入、修改或刪除資料來源的**SQLConfigDataSource**函數會使用下列關鍵字。  
  
|關鍵字|描述|  
|-------------|-----------------|  
|DBQ|若為 Microsoft Excel 驅動程式，則在存取 Microsoft Excel 5.0 或更新版本的檔案時，為活頁簿檔案的名稱。<br /><br /> 這會在 [安裝程式] 對話方塊中設定與**資料庫**相同的選項。|  
|DEFAULTDIR|目錄的路徑規格。<br /><br /> 這會將相同的選項設定為 [**選取目錄**]，或在 [安裝] 對話方塊中選取 [活頁**簿**]。|  
|DESCRIPTION|資料來源中的資料描述。<br /><br /> 這會在 [安裝程式] 對話方塊中設定與 [**描述**] 相同的選項。|  
|DRIVER|驅動程式 DLL 的路徑規格。|  
|DRIVERID|驅動程式的整數識別碼。<br /><br /> 534（Microsoft Excel 3.0）<br /><br /> 278（Microsoft Excel 4.0）<br /><br /> 22（Microsoft Excel 5.0/7.0）<br /><br /> 790（Microsoft Excel 97-2003）|  
|FIL|檔案類型，例如 Excel 3.0、Excel 4.0、Excel 5.0、Excel 7.0、Excel 97、Excel 2000 或 Excel 2003。|  
|FIRSTROWHASNAMES|指出範圍的第一個資料列的資料格是否包含資料表的資料行名稱（1）或 not （0）。|  
|MAXSCANROWS|根據現有的資料來設定資料行的資料類型時，所要掃描的資料列數目。<br /><br /> 可以輸入從1到16的數位，以供要掃描的資料列使用。 值預設為 8;如果設定為0，則會掃描所有資料列。 （超出限制的數位將會傳回錯誤）。<br /><br /> 這會在 [安裝程式] 對話方塊中，設定與**要掃描**的資料列相同的選項。|  
|READONLY|TRUE 表示將檔案設為唯讀;FALSE 表示讓檔案不是唯讀的。<br /><br /> 這會在 [安裝程式] 對話方塊中設定與 [**唯讀**] 相同的選項。|  
|串接|要使用之引擎的背景執行緒數目。 若為 Microsoft Access 驅動程式，此值預設為3，但可以變更。 對於 dBASE 而言，MicrosoftExceldriver 此值為3，且無法變更。<br /><br /> 這會在 [安裝程式] 對話方塊中設定與**執行緒**相同的選項。|
