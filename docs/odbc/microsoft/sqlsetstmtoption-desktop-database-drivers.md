---
title: SQLSetStmtOption(桌面資料庫驅動程式) |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299408"
---
# <a name="sqlsetstmtoption-desktop-database-drivers"></a>SQLSetStmtOption (桌面資料庫驅動程式)

|*fOption*|註解|  
|---------------|--------------|  
|SQL_ASYNC_ENABLE|不支持非同步處理。 SQL_ASYNC_ENABLE fOption 將傳回 SQLSTATE S1C00(驅動程式無法使用)。|  
|SQL_KEYSET_SIZE|唯一有效的鍵集大小為 0,因為不支援混合游標和動態游標。 如果此值設置為任何其他號碼,它將更改為 0,並且調用將返回SQL_SUCCESS_WITH_INFO和 SQLSTATE 01S02(選項值已更改)。|  
|SQL_MAX_ROWS|唯一有效的行集大小為 0,因為桌面資料庫驅動程式不支援限制返回的行數。 如果此值設置為任何其他號碼,它將更改為 0,並且調用將返回SQL_SUCCESS_WITH_INFO和 SQLSTATE 01S02(選項值已更改)。|  
|SQL_QUERY_TIMEOUT|不支援。|  
|SQL_ROW_NUMBER|不支援。|  
|SQL_SIMULATE_CURSOR|不支援。|
