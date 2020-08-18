---
description: SQLConfigDataSource (文字檔驅動程式)
title: SQLConfigDataSource (文字檔驅動程式) |Microsoft Docs
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
ms.openlocfilehash: 400b83d382140d4661b103e24449f14ecdfda43d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411864"
---
# <a name="sqlconfigdatasource-text-file-driver"></a>SQLConfigDataSource (文字檔驅動程式)
> [!NOTE]  
>  本主題提供文字檔驅動程式特定的資訊。 如需此函數的一般資訊，請參閱 [ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的適當主題。  
  
 用來動態加入、修改或刪除資料來源的 **SQLConfigDataSource** 函數會使用下列關鍵字。  
  
|關鍵字|描述|  
|-------------|-----------------|  
|CHARACTERSET|適用于文字驅動程式、OEM 或 ANSI。|  
|COLNAMEHEADER|如果是 Text 驅動程式，則表示資料的第一筆記錄是否會指定資料行名稱。 是 TRUE 或 FALSE。|  
|DEFAULTDIR|目錄的路徑規格。|  
|DESCRIPTION|資料來源中資料的描述。<br /><br /> 這會將相同的選項設定為 [安裝] 對話方塊中的 [ **描述** ]。|  
|DRIVER|驅動程式 DLL 的路徑規格。|  
|DRIVERID|驅動程式的整數識別碼。 27 (文字) |  
|擴展|列出資料來源上文字檔的副檔名。<br /><br /> 這會在 [設定] 對話方塊中設定與 **擴充功能清單** 相同的選項。|  
|FIL|檔案類型文字|  
|FILETYPE|Text 驅動程式的檔案類型 (文字) 。|  
|FORMAT|針對文字驅動程式，可以是 FIXEDLENGTH、TABDELIMITED、CSVDELIMITED (（由逗號) ）或以括弧) 中指定的特殊字元分隔 ( # A3 (。 特殊字元的長度是一個字元，而且可以是字元、十進位或十六進位格式。|  
|MAXSCANROWS|根據現有資料設定資料行的資料類型時，所要掃描的資料列數目。<br /><br /> 針對文字驅動程式，您可以輸入從1到32767的數位，以掃描的資料列數目;不過，此值一律會預設為25。  (超出限制的數位將會傳回錯誤。 ) <br /><br /> 這會將相同的選項設定為要在 [設定] 對話方塊中掃描的資料 **列** 。|  
|READONLY|TRUE 表示將檔案設為唯讀;FALSE 表示讓檔案不是唯讀的。<br /><br /> 這會將相同的選項設定為 [安裝] 對話方塊中的 [ **唯讀** ]。|
