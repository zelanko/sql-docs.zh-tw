---
description: ODBC 驅動程式子機碼
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b950a352c3da69a2a8de9a89f7bbebf87e0a597a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448918"
---
# <a name="odbc-drivers-subkey"></a>ODBC 驅動程式子機碼
ODBC 驅動程式子機碼底下的值會列出已安裝的驅動程式。 這些值的格式如下表所示。  
  
|名稱|資料類型|資料|  
|----------|---------------|----------|  
|*驅動程式-描述*|REG_SZ|**已安裝**|  
  
 *驅動程式描述*名稱是由驅動程式開發人員定義。 這通常是與驅動程式相關聯的 DBMS 名稱。  
  
 例如，假設已針對格式化的文字檔和 SQL Server 安裝驅動程式。 ODBC 驅動程式子機碼底下的值可能是：  
  
```  
Text : REG_SZ : Installed  
SQL Server : REG_SZ : Installed  
```
