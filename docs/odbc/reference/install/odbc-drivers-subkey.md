---
title: ODBC 驅動程式子鍵 :微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304029"
---
# <a name="odbc-drivers-subkey"></a>ODBC 驅動程式子機碼
ODBC 驅動程式下鍵下的值列出了已安裝的驅動程式。 這些值的格式顯示在下表中。  
  
|名稱|資料類型|資料|  
|----------|---------------|----------|  
|*驅動程式描述*|REG_SZ|**安裝**|  
  
 *驅動程式描述*名稱由驅動程式開發人員定義。 它通常是與驅動程式關聯的 DBMS 的名稱。  
  
 例如,假設已為格式化的文本檔和 SQL Server 安裝了驅動程式。 ODBC 驅動程式子鍵下的值可能是:  
  
```  
Text : REG_SZ : Installed  
SQL Server : REG_SZ : Installed  
```
