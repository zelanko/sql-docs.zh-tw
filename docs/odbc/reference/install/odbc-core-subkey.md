---
title: ODBC Core 子機碼 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], core subkey
- registry entries for components [ODBC], core subkey
- core subkey [ODBC]
ms.assetid: 055b31fc-f96c-450b-a596-d4570079fbf2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f05e36c59d674104dead92ecd7da63f5fb58588a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32916063"
---
# <a name="odbc-core-subkey"></a>ODBC Core 子機碼
ODBC Core 子機碼下的值提供的核心元件 （驅動程式管理員、 資料指標程式庫，安裝程式的 DLL，等等） 的使用計數。 下表顯示此值的格式。  
  
|名稱|資料類型|資料|  
|----------|---------------|----------|  
|UsageCount|REG_DWORD|*計數*|  
  
 例如，假設已由三個不同的應用程式和兩個不同的驅動程式的安裝程式安裝的 ODBC 核心元件。 ODBC Core 子機碼下的值會是：  
  
```  
UsageCount : REG_DWORD : 0x5  
```
