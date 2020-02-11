---
title: ODBC Core 子機碼 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 98c9380083eb5a0ad796f436af271564676b757d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68094013"
---
# <a name="odbc-core-subkey"></a>ODBC 核心子機碼
ODBC Core 子機碼底下的值提供核心元件的使用計數（驅動程式管理員、資料指標程式庫、安裝程式 DLL 等等）。 下表顯示此值的格式。  
  
|名稱|資料類型|資料|  
|----------|---------------|----------|  
|UsageCount|REG_DWORD|*計數*|  
  
 例如，假設 ODBC Core 元件是由三個不同應用程式的安裝程式和兩個不同的驅動程式所安裝。 ODBC Core 子機碼底下的值會是：  
  
```  
UsageCount : REG_DWORD : 0x5  
```
