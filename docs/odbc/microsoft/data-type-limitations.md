---
description: 資料類型限制
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
ms.openlocfilehash: 4853846f21aa0ad763295bbdc4233c472ac53864
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412784"
---
# <a name="data-type-limitations"></a>資料類型限制
Microsoft ODBC Desktop 資料庫驅動程式會對資料類型強加下列限制：  
  
|資料類型|描述|  
|---------------|-----------------|  
|所有資料類型|類型轉換失敗可能會導致受影響的資料行設定為 Null。|  
|BINARY|建立零長度的二進位資料行實際上會傳回255位元組的二進位資料行。|  
|日期|DATE 資料類型無法轉換成另一種資料類型 (或由 CONVERT 函數) 。|  
|DECIMAL (精確數值) |不支援。|  
|浮點數資料類型|浮點數中的小數位數可能會受限於 Windows 主控台的國際區段中設定的數位格式。|  
|NUMERIC|支援最大精確度和小數位數28。|  
|timestamp|CONVERT 函數無法將時間戳記資料類型轉換成本身。|  
|TINYINT|TINYINT 值一律不帶正負號。|  
|長度為零的字串|使用 dBASE、Microsoft Excel、Paradox 或 Textdriver 時，在資料行中插入長度為零的字串實際上會插入 Null。|
