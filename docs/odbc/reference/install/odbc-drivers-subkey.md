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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dd1f8d3293e35a543cce6b5079d9c6e10a331a88
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304029"
---
# <a name="odbc-drivers-subkey"></a>ODBC 驅動程式子機碼
ODBC 驅動程式子機碼底下的值會列出已安裝的驅動程式。 下表顯示這些值的格式。  
  
|名稱|資料類型|資料|  
|----------|---------------|----------|  
|*驅動程式-描述*|REG_SZ|**已安裝**|  
  
 驅動程式的*描述*名稱是由驅動程式開發人員所定義。 這通常是與驅動程式相關聯的 DBMS 名稱。  
  
 例如，假設已針對格式化的文字檔和 SQL Server 安裝驅動程式。 ODBC 驅動程式子機碼下的值可能是：  
  
```  
Text : REG_SZ : Installed  
SQL Server : REG_SZ : Installed  
```
