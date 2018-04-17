---
title: ODBC 驅動程式的子機碼 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- subkeys [ODBC], drivers subkey
- registry entries for components [ODBC], drivers subkey
- drivers subkey [ODBC]
ms.assetid: 8edbf68f-d05d-4d77-92f6-e9500008f520
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 925e24f295602d7e66fe37935b53724b4d162adf
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="odbc-drivers-subkey"></a>ODBC 驅動程式的子機碼
ODBC 驅動程式的子機碼下的值會列出已安裝的驅動程式。 下表顯示這些值的格式。  
  
|名稱|資料類型|資料|  
|----------|---------------|----------|  
|*驅動程式說明*|REG_SZ|**安裝**|  
  
 *驅動程式描述*驅動程式開發人員所定義名稱。 它通常是與驅動程式相關聯的 DBMS 名稱。  
  
 例如，假設已格式化的文字檔案和 SQL Server 安裝的驅動程式。 ODBC 驅動程式的子機碼下的值可能是：  
  
```  
Text : REG_SZ : Installed  
SQL Server : REG_SZ : Installed  
```
