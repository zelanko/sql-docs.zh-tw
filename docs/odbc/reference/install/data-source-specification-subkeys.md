---
title: 資料源規範子金鑰 |微軟文件
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
ms.openlocfilehash: 281377c307f3f3750e87bf5dc988beb7660067af
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300338"
---
# <a name="data-source-specification-subkeys"></a>資料來源規格子機碼
ODBC 資料源子鍵中列出的每個數據源都有其自己的子密鑰。 此子鍵的名稱與 ODBC 數據源子鍵下的相應值相同。 此子鍵下的值必須列出驅動程式 DLL,並可以列出數據源的說明。 如果驅動程式支援轉換器,則值可以列出預設轉換器的名稱、預設翻譯 DLL 和預設翻譯選項。 這些值還可以列出驅動程式連接到數據源所需的其他資訊。 例如,驅動程式可能需要伺服器名稱、資料庫名稱或架構名稱。  
  
 值的格式如下表所示。 僅需要驅動程式值。  
  
|名稱|資料類型|資料|  
|----------|---------------|----------|  
|描述|REG_SZ|*描述*|  
|驅動程式|REG_SZ|*驅動程式-DLL 路徑*|  
|翻譯DLL|REG_SZ|*轉換器-DLL 路徑*|  
|翻譯名稱|REG_SZ|*翻譯人名稱*|  
|翻譯選項|REG_SZ|*翻譯選項*|  
|*選擇值名稱*|*選擇價值型態*|*選擇價值資料*|  
  
 例如,假設 SQL Server 驅動程式需要伺服器名稱和 OEM 到 ANSI 轉換的標誌,並為這些轉換定義伺服器和 OEMTOANSI 值。 還假設清單數據源使用 Microsoft®代碼頁轉換器在 Windows®拉丁文 1 (1250) 和多語言 (850) 代碼頁之間進行翻譯。 "庫存子"項下的值可能如下所示:  
  
```  
Description : REG_SZ : Inventory database on server InvServ  
Driver : REG_SZ : C:\WINDOWS\SYSTEM32\SQLSRV32.DLL  
OEMTOANSI : REG_SZ : Yes  
Server : REG_SZ : InvServ  
TranslationDLL : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
TranslationName : REG_SZ : MS Code Page Translator  
TranslationOption : REG_SZ : 12500850  
```
