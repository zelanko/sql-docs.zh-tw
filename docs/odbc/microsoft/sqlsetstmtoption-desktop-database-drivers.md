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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 48dc5dff83e942b894548d44e3673c19ca0746c5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63305799"
---
# <a name="sqlsetstmtoption-desktop-database-drivers"></a>SQLSetStmtOption (桌面資料庫驅動程式)

|*fOption*|註解|  
|---------------|--------------|  
|SQL_ASYNC_ENABLE|不支援非同步處理。 SQL_ASYNC_ENABLE fOption 會傳回 SQLSTATE S1C00 （驅動程式不支援）。|  
|SQL_KEYSET_SIZE|唯一有效的索引鍵集大小為 0，因為混用，並不支援動態資料指標。 如果此值設定為其他任何數字，它就會變更為 0，並呼叫會傳回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01s02 的警告 （選項值已變更）。|  
|SQL_MAX_ROWS|唯一有效的資料列集大小為 0，因為桌面資料庫驅動程式不支援限制傳回的資料列數目。 如果此值設定為其他任何數字，它就會變更為 0，並呼叫會傳回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01s02 的警告 （選項值已變更）。|  
|SQL_QUERY_TIMEOUT|不支援。|  
|SQL_ROW_NUMBER|不支援。|  
|SQL_SIMULATE_CURSOR|不支援。|
