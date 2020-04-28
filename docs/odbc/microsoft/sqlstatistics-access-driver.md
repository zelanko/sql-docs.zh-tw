---
title: SQLStatistics （Access 驅動程式） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLStatistics
- SQLStatistics function [ODBC], Access Driver
ms.assetid: 6117ac77-1020-4f0c-8eed-e671c34c1f21
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f75f41bf63cbf224772955effa0f120b5d384111
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299358"
---
# <a name="sqlstatistics-access-driver"></a>SQLStatistics (Access 驅動程式)
> [!NOTE]  
>  本主題提供存取驅動程式特定的資訊。 如需此函數的一般資訊，請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)底下的適當主題。  
  
|資料行|評價|  
|------------|--------------|  
|TABLE_QUALIFIER|針對 Microsoft Access，會傳回資料庫檔案的路徑。<br /><br /> *SzTableQualifier*引數中不支援模式比對。|  
|TABLE_OWNER|此資料行中會傳回 Null，因為不支援擁有者名稱。|  
|TABLE_NAME|未分隔資料表名稱。<br /><br /> *SzTableName*引數中不支援模式比對。|  
|INDEX_QUALIFIER|一律會傳回 Null。|  
|INDEX_NAME|索引相依。|  
|TYPE|只有 SQL_TABLE_STAT 或 SQL_INDEX_OTHER 會針對類型傳回。|  
|SEQ_IN_INDEX|索引相依。|  
|COLUMN_NAME|索引相依。|  
|COLLATION|索引相依。|  
|CARDINALITY|僅針對 Microsoft Access 傳回。|  
|PAGES|一律會傳回 Null。|  
  
 篩選是以唯一性（ *fUnique*引數）為基礎。 *FAccuracy*參數會被忽略。
