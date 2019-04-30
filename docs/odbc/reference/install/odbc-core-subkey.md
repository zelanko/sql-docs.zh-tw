---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5c95c4e28a5f32131307daeaa61e214af887b577
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63069695"
---
# <a name="odbc-core-subkey"></a>ODBC 核心子機碼
ODBC 核心子機碼下的值提供的核心元件 （驅動程式管理員、 資料指標程式庫、 安裝程式 DLL，等等） 的使用計數。 下表顯示此值的格式。  
  
|名稱|資料類型|資料|  
|----------|---------------|----------|  
|UsageCount|REG_DWORD|*計數*|  
  
 例如，假設為三個不同的應用程式和兩個不同的驅動程式安裝程式已安裝的 ODBC 核心元件。 ODBC 核心子機碼下的值會是：  
  
```  
UsageCount : REG_DWORD : 0x5  
```
