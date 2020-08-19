---
description: SQLStatistics (dBASE 驅動程式)
title: SQLStatistics (dBASE 驅動程式) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLStatistics function [ODBC], dBASE Driver
- DBase driver [ODBC], SQLStatistics
ms.assetid: 631cec1b-66b7-4103-b9a7-ffd81da3c442
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9285f78bbafb7594e3a9cbab2845cedeff0c1af9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421562"
---
# <a name="sqlstatistics-dbase-driver"></a>SQLStatistics (dBASE 驅動程式)
> [!NOTE]  
>  本主題提供 dBASE 驅動程式特定的資訊。 如需此函數的一般資訊，請參閱 [ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的適當主題。  
  
|資料行|註解|  
|------------|--------------|  
|TABLE_QUALIFIER|目錄的路徑。<br /><br /> *SzTableQualifier*引數不支援模式比對。|  
|TABLE_OWNER|因為不支援擁有者名稱，所以會在此資料行中傳回 Null。|  
|TABLE_NAME|未分隔資料表名稱。<br /><br /> *SzTableName*引數不支援模式比對。|  
|INDEX_QUALIFIER|一律會傳回 Null。|  
|INDEX_NAME|索引相依。|  
|TYPE|只會傳回類型的 SQL_TABLE_STAT 或 SQL_INDEX_OTHER。|  
|SEQ_IN_INDEX|索引相依。|  
|COLUMN_NAME|索引相依。|  
|COLLATION|索引相依。|  
|PAGES|一律會傳回 Null。|  
  
 篩選是根據 (*fUnique* 引數) 的唯一性。 *FAccuracy*參數會被忽略。
