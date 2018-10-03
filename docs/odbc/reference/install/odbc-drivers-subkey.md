---
title: ODBC 驅動程式子機碼 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], drivers subkey
- registry entries for components [ODBC], drivers subkey
- drivers subkey [ODBC]
ms.assetid: 8edbf68f-d05d-4d77-92f6-e9500008f520
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 43be1c5e75998903ff4e64fc5f4230818a873ffc
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47772016"
---
# <a name="odbc-drivers-subkey"></a>ODBC 驅動程式子機碼
ODBC 驅動程式子機碼下的值會列出已安裝的驅動程式。 下表顯示這些值的格式。  
  
|名稱|資料類型|data|  
|----------|---------------|----------|  
|*驅動程式說明*|REG_SZ|**安裝**|  
  
 *驅動程式說明*驅動程式開發人員所定義名稱。 它通常是與驅動程式相關聯的 DBMS 名稱。  
  
 例如，假設已格式化的文字檔案和 SQL Server 安裝的驅動程式。 可能的 ODBC 驅動程式子機碼底下的值：  
  
```  
Text : REG_SZ : Installed  
SQL Server : REG_SZ : Installed  
```
