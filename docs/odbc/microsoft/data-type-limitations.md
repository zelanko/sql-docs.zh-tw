---
title: 資料類型的限制 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d4ce0eb96832f4a6b9c1953b0a9a9d0af65cb3b0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63187438"
---
# <a name="data-type-limitations"></a>資料類型限制
Microsoft ODBC 桌面資料庫驅動程式以強制資料類型有以下限制：  
  
|資料類型|描述|  
|---------------|-----------------|  
|所有的資料類型|類型轉換失敗可能會造成影響的資料行設為 NULL。|  
|BINARY|建立零長度的二進位資料行時，實際上會傳回 255 個位元組的二進位資料行。|  
|DATE|DATE 資料類型無法轉換成另一種資料類型 （或本身），由轉換函式。|  
|十進位 （精確數值）|不支援。|  
|浮點資料類型|浮點數中的小數位數可能會受限於數字格式的 Windows 控制台中的國際區段中設定。|  
|NUMERIC|支援最大有效位數和小數位數 28。|  
|timestamp|TIMESTAMP 資料類型無法轉換以本身，CONVERT 函式。|  
|TINYINT|TINYINT 值一律是不帶正負號。|  
|零長度字串|DBASE、 Microsoft Excel、 Paradox、 或 Textdriver 使用時，長度為零的字串插入資料行實際插入 null 值改為。|
