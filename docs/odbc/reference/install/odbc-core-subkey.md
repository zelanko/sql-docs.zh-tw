---
description: ODBC 核心子機碼
title: ODBC 核心子機碼 |Microsoft Docs
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
ms.openlocfilehash: 37948c46d6a717975902bc2109ece2aea02b0129
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499733"
---
# <a name="odbc-core-subkey"></a>ODBC 核心子機碼
ODBC Core 子機碼底下的值會提供核心元件的使用計數 (驅動程式管理員、資料指標程式庫、安裝程式 DLL 等等) 。 下表顯示此值的格式。  
  
|名稱|資料類型|資料|  
|----------|---------------|----------|  
|UsageCount|REG_DWORD|*計數*|  
  
 例如，假設安裝程式已針對三個不同的應用程式和兩個不同的驅動程式安裝 ODBC 核心元件。 ODBC 核心子機碼底下的值為：  
  
```  
UsageCount : REG_DWORD : 0x5  
```
