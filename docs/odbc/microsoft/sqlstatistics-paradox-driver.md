---
title: SQLStatistics （Paradox 驅動程式） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Paradox driver [ODBC], SQLStatistics
- SQLStatistics function [ODBC], Paradox Driver
ms.assetid: 886cab83-d599-4fbc-9c88-e8cb833aac4b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5e9782eb22e4176a57aab7bdd3823982575a0d55
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299318"
---
# <a name="sqlstatistics-paradox-driver"></a>SQLStatistics (Paradox 驅動程式)
> [!NOTE]  
>  本主題提供 Paradox 驅動程式特有的資訊。 如需此函數的一般資訊，請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)底下的適當主題。  
  
|資料行|評價|  
|------------|--------------|  
|TABLE_QUALIFIER|目錄的路徑。<br /><br /> *SzTableQualifier*引數中不支援模式比對。|  
|TABLE_OWNER|此資料行中會傳回 Null，因為不支援擁有者名稱。|  
|TABLE_NAME|未分隔資料表名稱。<br /><br /> *SzTableName*引數中不支援模式比對。|  
|INDEX_QUALIFIER|一律會傳回 Null。|  
|INDEX_NAME|索引相依。|  
|TYPE|只有 SQL_TABLE_STAT 或 SQL_INDEX_OTHER 會針對類型傳回。|  
|SEQ_IN_INDEX|索引相依。|  
|COLUMN_NAME|索引相依。|  
|COLLATION|索引相依。|  
|PAGES|一律會傳回 Null。|  
  
 篩選是以唯一性（ *fUnique*引數）為基礎。 *FAccuracy*參數會被忽略。
