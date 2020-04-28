---
title: SQLSetStmtOption （桌面資料庫驅動程式） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetStmtOption function [ODBC], Desktop Database Drivers
ms.assetid: 98db9631-eb9b-4962-abe4-96f495133a5d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 69b386aee3f95fd047f72510dce7658130ac7aa5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299408"
---
# <a name="sqlsetstmtoption-desktop-database-drivers"></a>SQLSetStmtOption (桌面資料庫驅動程式)

|*fOption*|評價|  
|---------------|--------------|  
|SQL_ASYNC_ENABLE|不支援非同步處理。 SQL_ASYNC_ENABLE fOption 會傳回 SQLSTATE S1C00 （驅動程式不支援）。|  
|SQL_KEYSET_SIZE|唯一有效的索引鍵集大小為0，因為不支援混合和動態資料指標。 如果此值設定為任何其他數位，則會變更為0，而且呼叫會傳回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01S02 （選項值已變更）。|  
|SQL_MAX_ROWS|唯一有效的資料列集大小為0，因為桌面資料庫驅動程式不支援限制傳回的資料列數目。 如果此值設定為任何其他數位，則會變更為0，而且呼叫會傳回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01S02 （選項值已變更）。|  
|SQL_QUERY_TIMEOUT|不支援。|  
|SQL_ROW_NUMBER|不支援。|  
|SQL_SIMULATE_CURSOR|不支援。|
