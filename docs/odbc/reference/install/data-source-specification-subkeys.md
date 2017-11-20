---
title: "資料來源規格子機碼 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data source specification subkeys [ODBC]
- registry entries for data sources [ODBC], data source specification subkeys
- subkeys [ODBC], data source specification subkeys
ms.assetid: d7e88a07-e6ab-4258-a45d-1ca21234fbec
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 61b485f55be504e894754f74c4ab779b9ebbaf5a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="data-source-specification-subkeys"></a>資料來源規格子機碼
ODBC 資料來源的子機碼中所列每個資料來源都有自己的子機碼。 這個子機碼有同名的 ODBC 資料來源的子機碼下的對應值。 這個子機碼下的值必須列出驅動程式 DLL，而且可能會列出資料來源的描述。 如果驅動程式支援的轉譯器，這些值可能會列出預設轉譯程式預設轉譯 DLL 及預設轉譯選項的名稱。 值可能也會列出其他驅動程式連接到資料來源所需的資訊。 例如，驅動程式可能需要伺服器名稱、 資料庫名稱或結構描述名稱。  
  
 值的格式是下表所示。 需要的驅動程式值。  
  
|名稱|資料類型|data|  
|----------|---------------|----------|  
|Description|REG_SZ|*描述*|  
|驅動程式|REG_SZ|*驅動程式 DLL 路徑*|  
|TranslationDLL|REG_SZ|*轉譯程式 DLL 路徑*|  
|TranslationName|REG_SZ|*轉譯程式名稱*|  
|TranslationOption|REG_SZ|*轉譯選項*|  
|*選擇值名稱*|*選擇加入實值型別*|*選擇數值資料*|  
  
 例如，假設 SQL Server 驅動程式 ANSI 轉換 oem 所需的伺服器名稱和旗標，而這些定義的伺服器和 OEMTOANSI 值。 另外，假設，清查資料來源會使用 Microsoft® 程式碼頁面轉譯器，在 Windows® Latin 1 (1250) 與多語系 (850) 字碼頁之間轉譯。 清查子機碼下的值可能如下所示：  
  
```  
Description : REG_SZ : Inventory database on server InvServ  
Driver : REG_SZ : C:\WINDOWS\SYSTEM32\SQLSRV32.DLL  
OEMTOANSI : REG_SZ : Yes  
Server : REG_SZ : InvServ  
TranslationDLL : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
TranslationName : REG_SZ : MS Code Page Translator  
TranslationOption : REG_SZ : 12500850  
```

