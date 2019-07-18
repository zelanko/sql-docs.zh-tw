---
title: ODBC 資料來源的子機碼 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], for data sources
- data sources [ODBC], subkeys
- registry entries for data sources [ODBC], subkeys
ms.assetid: 0a8ccb80-c573-4418-84e5-f04a2b0e2ac1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2a1d0c506c4a4b33d7138378032947821d4e9f3e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68093996"
---
# <a name="odbc-data-sources-subkey"></a>ODBC 資料來源子機碼
ODBC 資料來源的子機碼下的值清單的資料來源。 這些值的格式會是下表所示。  
  
|名稱|資料類型|Data|  
|----------|---------------|----------|  
|*data-source-name*|REG_SZ|*driver-description*|  
  
 *資料來源名稱*值由管理程式 （這通常是它會提示使用者），定義並*驅動程式說明*驅動程式開發人員所定義 (通常是名稱DBMS 相關聯的驅動程式)。  
  
 例如，假設有三個資料來源已定義：清查，它會使用 SQL Server;薪資、 使用 dBASE;和人員，使用格式化的文字檔案。 ODBC 資料來源的子機碼下的值可能如下所示：  
  
```  
Inventory : REG_SZ : SQL Server  
Payroll : REG_SZ : dBASE  
Personnel : REG_SZ : Text  
```
