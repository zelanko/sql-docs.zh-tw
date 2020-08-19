---
description: ODBC 資料來源子機碼
title: ODBC 資料來源子機碼 |Microsoft Docs
ms.custom: ''
ms.date: 09/23/2019
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9897c68d110f59d03ac8e1b3e403ed21844082fb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448930"
---
# <a name="odbc-data-sources-subkey"></a>ODBC 資料來源子機碼

子機碼底下的值會 `ODBC Data Sources` 列出資料來源。 這些值的格式如下表所示。

| 名稱 | 資料類型 | 資料 |
| :--- | :-------- | :--- |
| *資料來源名稱* | REG_SZ | *驅動程式-描述* |
| &nbsp; | &nbsp; | &nbsp; |

*資料來源名稱*值是由管理程式所定義 (這通常會提示使用者進行) ，而*驅動程式描述*是由驅動程式開發人員定義 (這通常是與驅動程式) 相關聯之 DBMS 的名稱。

例如，假設已定義三個數據源：使用 SQL Server 的清查：使用 dBASE 的薪資;以及使用格式化文字檔的人員。 子機碼底下的值可能如下所示 `ODBC Data Sources` ：

```console
Inventory : REG_SZ : SQL Server
Payroll : REG_SZ : dBASE
Personnel : REG_SZ : Text
```
