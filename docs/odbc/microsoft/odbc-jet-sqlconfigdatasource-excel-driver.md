---
description: ODBC Jet SQLConfigDataSource (Excel 驅動程式)
title: ODBC Jet SQLConfigDataSource (Excel 驅動程式) |Microsoft Docs
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
ms.openlocfilehash: 61fcc1e7df00f14a7b92e294262b7806382a3d52
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500301"
---
# <a name="odbc-jet-sqlconfigdatasource-excel-driver"></a>ODBC Jet SQLConfigDataSource (Excel 驅動程式)
> [!NOTE]  
>  本主題提供 Excel 驅動程式特定的資訊。 如需此函數的一般資訊，請參閱 [ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的適當主題。  
  
 用來動態加入、修改或刪除資料來源的 **SQLConfigDataSource** 函數會使用下列關鍵字。  
  
|關鍵字|描述|  
|-------------|-----------------|  
|DBQ|若為 Microsoft Excel 驅動程式，則在存取 Microsoft Excel 5.0 或更新版本的檔案時，是活頁簿檔案的名稱。<br /><br /> 這會將相同的選項設定為 [安裝] 對話方塊中的 [ **資料庫** ]。|  
|DEFAULTDIR|目錄的路徑規格。<br /><br /> 這會設定與 [ **選取目錄** ] 相同的選項，或在 [安裝程式] 對話方塊中選取 [活頁 **簿** ]。|  
|DESCRIPTION|資料來源中資料的描述。<br /><br /> 這會將相同的選項設定為 [安裝] 對話方塊中的 [ **描述** ]。|  
|DRIVER|驅動程式 DLL 的路徑規格。|  
|DRIVERID|驅動程式的整數識別碼。<br /><br /> 534 (Microsoft Excel 3.0) <br /><br /> 278 (Microsoft Excel 4.0) <br /><br /> 22 (Microsoft Excel 5.0/7.0) <br /><br /> 790 (Microsoft Excel 97-2003) |  
|FIL|檔案類型，例如 Excel 3.0、Excel 4.0、Excel 5.0、Excel 7.0、Excel 97、Excel 2000 或 Excel 2003。|  
|FIRSTROWHASNAMES|指出範圍中第一個資料列的資料格是否包含資料表 (1) 的資料行名稱，或 (0) 。|  
|MAXSCANROWS|根據現有資料設定資料行的資料類型時，所要掃描的資料列數目。<br /><br /> 您可以輸入從1到16的數位來掃描資料列。 值預設為 8;如果設定為0，則會掃描所有資料列。  (超出限制的數位將會傳回錯誤。 ) <br /><br /> 這會將相同的選項設定為要在 [設定] 對話方塊中掃描的資料 **列** 。|  
|READONLY|TRUE 表示將檔案設為唯讀;FALSE 表示讓檔案不是唯讀的。<br /><br /> 這會將相同的選項設定為 [安裝] 對話方塊中的 [ **唯讀** ]。|  
|執行緒|引擎要使用的背景執行緒數目。 若為 Microsoft Access 驅動程式，此值預設為3，但可以變更。 針對 dBASE，MicrosoftExceldriver 此值為3，而且無法變更。<br /><br /> 這會將相同的選項設定為 [設定] 對話方塊中的 [ **執行緒** ]。|
