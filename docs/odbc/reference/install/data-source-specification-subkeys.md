---
description: 資料來源規格子機碼
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8fabfd07779f74945bf647d20075de0cc057710b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494563"
---
# <a name="data-source-specification-subkeys"></a>資料來源規格子機碼
ODBC 資料來源子機碼中列出的每個資料來源都有自己的子機碼。 這個子機碼與 [ODBC 資料來源] 子機碼下的對應值具有相同的名稱。 此子機碼底下的值必須列出驅動程式 DLL，而且可能會列出資料來源的描述。 如果驅動程式支援轉譯器，這些值可能會列出預設翻譯工具的名稱、預設轉譯 DLL 和預設轉譯選項。 這些值也可以列出驅動程式連接到資料來源所需的其他資訊。 例如，驅動程式可能需要伺服器名稱、資料庫名稱或架構名稱。  
  
 值的格式如下表所示。 只有驅動程式值是必要的。  
  
|名稱|資料類型|資料|  
|----------|---------------|----------|  
|描述|REG_SZ|*description*|  
|驅動程式|REG_SZ|*驅動程式-DLL-路徑*|  
|TranslationDLL|REG_SZ|*translator-DLL-path*|  
|TranslationName|REG_SZ|*translator-名稱*|  
|TranslationOption|REG_SZ|*轉譯-選項*|  
|*選擇值名稱*|*opt-數值型別*|*opt-值-資料*|  
  
 例如，假設 SQL Server 驅動程式需要伺服器名稱以及 OEM 至 ANSI 轉換的旗標，並定義伺服器和 OEMTOANSI 的值。 另外，假設清查資料來源使用 Microsoft®字碼頁翻譯工具，在 Windows®拉丁 1 (1250) 和多語系 (850) 字碼頁之間轉譯。 清查子機碼底下的值可能如下所示：  
  
```  
Description : REG_SZ : Inventory database on server InvServ  
Driver : REG_SZ : C:\WINDOWS\SYSTEM32\SQLSRV32.DLL  
OEMTOANSI : REG_SZ : Yes  
Server : REG_SZ : InvServ  
TranslationDLL : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
TranslationName : REG_SZ : MS Code Page Translator  
TranslationOption : REG_SZ : 12500850  
```
