---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4d6d54d1fc7c7742bf94e91d7370f356e28b5624
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "71207683"
---
# <a name="odbc-data-sources-subkey"></a>ODBC 資料來源子機碼

子機碼底下`ODBC Data Sources`的值會列出資料來源。 下表顯示這些值的格式。

| 名稱 | 資料類型 | 資料 |
| :--- | :-------- | :--- |
| *資料-來源-名稱* | REG_SZ | *驅動程式-描述* |
| &nbsp; | &nbsp; | &nbsp; |

[*資料來源名稱*] 值是由管理程式定義（通常會提示使用者），而*驅動程式描述*是由驅動程式開發人員定義（這通常是與驅動程式相關聯的 DBMS 名稱）。

例如，假設有三個數據源已定義：清查，這會使用 SQL Server;使用 dBASE 的薪資;和人員，其使用格式化的文字檔。 子機碼底下`ODBC Data Sources`的值可能如下所示：

```console
Inventory : REG_SZ : SQL Server
Payroll : REG_SZ : dBASE
Personnel : REG_SZ : Text
```
