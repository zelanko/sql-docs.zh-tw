---
title: ODBC 核心子鍵 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], core subkey
- registry entries for components [ODBC], core subkey
- core subkey [ODBC]
ms.assetid: 055b31fc-f96c-450b-a596-d4570079fbf2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9e6bfcf3c1efa87076e6d3e27a438cde6f794157
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304051"
---
# <a name="odbc-core-subkey"></a>ODBC 核心子機碼
ODBC Core 子鍵下的值提供核心元件(驅動程式管理器、游標庫、安裝程式 DLL 等)的使用計數。 此值的格式顯示在下表中。  
  
|名稱|資料類型|資料|  
|----------|---------------|----------|  
|使用方式計數|REG_DWORD|*count*|  
  
 例如,假設 ODBC Core 元件已由針對三個不同的應用程式和兩個不同的驅動程式的安裝程式安裝。 ODBC 核心子鍵下的值是:  
  
```  
UsageCount : REG_DWORD : 0x5  
```
