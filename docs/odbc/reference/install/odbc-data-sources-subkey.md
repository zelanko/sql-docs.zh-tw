---
title: ODBC 資料來源子鍵 :微軟文件
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
ms.openlocfilehash: c5e97e643a78187b15e91833c832cd16ca435c7f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304052"
---
# <a name="odbc-data-sources-subkey"></a>ODBC 資料來源子鍵

`ODBC Data Sources`子鍵下的值列出數據源。 這些值的格式顯示在下表中。

| 名稱 | 資料類型 | 資料 |
| :--- | :-------- | :--- |
| *資料來源名稱* | REG_SZ | *驅動程式描述* |
| &nbsp; | &nbsp; | &nbsp; |

*數據來源名稱*值由管理程式定義(通常提示用戶進行它),*驅動程式描述*由驅動程式開發人員定義(它通常是與驅動程式關聯的 DBMS 的名稱)。

例如,假設定義了三個數據源:使用 SQL Server 的清單;使用 dBASE 的薪資;和人員,它使用格式化的文本檔。 子鍵下`ODBC Data Sources`的值可能如下所示:

```console
Inventory : REG_SZ : SQL Server
Payroll : REG_SZ : dBASE
Personnel : REG_SZ : Text
```
