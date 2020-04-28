---
title: 資料類型限制 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], data types
- data types [ODBC], desktop database drivers
- desktop database drivers [ODBC], data types
ms.assetid: 81c4eab7-1f6b-47a0-b940-89d6c6a14dae
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4beaf91a4ead743e3e8a2e32578796baba3c17be
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81280668"
---
# <a name="data-type-limitations"></a>資料類型限制
Microsoft ODBC 桌面資料庫驅動程式會對資料類型施加下列限制：  
  
|資料類型|描述|  
|---------------|-----------------|  
|所有資料類型|類型轉換失敗可能會導致受影響的資料行設定為 Null。|  
|BINARY|建立長度為零的二進位資料行實際上會傳回255位元組的二進位資料行。|  
|日期|DATE 資料類型無法透過 CONVERT 函數轉換成另一個資料類型（或其本身）。|  
|DECIMAL （精確數值）|不支援。|  
|浮點資料類型|浮點數中的小數位數，可能會受限於 Windows [控制台] 的 [國際] 區段中設定的數位格式。|  
|NUMERIC|支援最大有效位數和小數位數28。|  
|timestamp|TIMESTAMP 資料類型無法透過 CONVERT 函數轉換成本身。|  
|TINYINT|TINYINT 值一律不帶正負號。|  
|長度為零的字串|使用 dBASE、Microsoft Excel、Paradox 或 Textdriver 時，將長度為零的字串插入資料行中，實際上會改為插入 Null。|
