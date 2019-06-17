---
title: 資料來源規格子機碼 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data source specification subkeys [ODBC]
- registry entries for data sources [ODBC], data source specification subkeys
- subkeys [ODBC], data source specification subkeys
ms.assetid: d7e88a07-e6ab-4258-a45d-1ca21234fbec
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ad210f91d00f9e692c8ee20fef01a808a01501c3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63198214"
---
# <a name="data-source-specification-subkeys"></a>資料來源規格子機碼
ODBC 資料來源的子機碼中所列每個資料來源都有自己的子機碼。 這個子機碼具有相同名稱做為 ODBC 資料來源的子機碼下對應的值。 這個子機碼底下的值都必須列出驅動程式 DLL，並可能會列出資料來源的描述。 如果驅動程式支援的轉譯器，值可能會列出預設轉譯器的預設轉譯 DLL 及預設轉譯選項的名稱。 值可能也會列出其他驅動程式連接到資料來源所需的資訊。 例如，驅動程式可能需要伺服器名稱、 資料庫名稱或結構描述名稱。  
  
 值的格式是下表所示。 需要驅動程式值。  
  
|名稱|資料類型|資料|  
|----------|---------------|----------|  
|描述|REG_SZ|*description*|  
|驅動程式|REG_SZ|*driver-DLL-path*|  
|TranslationDLL|REG_SZ|*translator-DLL-path*|  
|TranslationName|REG_SZ|*translator-name*|  
|TranslationOption|REG_SZ|*translation-option*|  
|*opt-value-name*|*opt-value-type*|*opt-value-data*|  
  
 例如，假設 SQL Server 驅動程式 ANSI 轉換為 OEM 所需的伺服器名稱和旗標，而這些定義的伺服器和 OEMTOANSI 值。 另外，假設，清查資料來源會使用 Microsoft® 程式碼頁面轉譯器，在多國語言 (850) 字碼頁與 Windows® Latin 1 (1250) 之間進行轉換。 清查子機碼下的值可能如下所示：  
  
```  
Description : REG_SZ : Inventory database on server InvServ  
Driver : REG_SZ : C:\WINDOWS\SYSTEM32\SQLSRV32.DLL  
OEMTOANSI : REG_SZ : Yes  
Server : REG_SZ : InvServ  
TranslationDLL : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
TranslationName : REG_SZ : MS Code Page Translator  
TranslationOption : REG_SZ : 12500850  
```
