---
title: SQLFetchScroll |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLFetchScroll function
ms.assetid: 524a3985-a08d-4445-99e0-bb551a666615
caps.latest.revision: 34
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 3b4c66991e69e9bdb8ca90d76aa81c5069c84f57
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36145138"
---
# <a name="sqlfetchscroll"></a>SQLFetchScroll
  **SQLFetchScroll**一個資料列集傳回到應用程式。 使用設定的資料列集大小[SQLSetStmtAttr](sqlsetstmtattr.md)。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式支援所有定義的提取指示 （例如，sql_fetch_relative），但具有下列限制：  
  
-   如果有針對陳述式而定義順向資料指標，則需要 SQL_FETCH_NEXT，而且以任何其他格式嘗試提取會導致錯誤傳回。  
  
-   僅針對靜態和索引鍵集導向的資料指標支援 SQL_FETCH_BOOKMARK。  
  
## <a name="sqlfetchscroll-support-for-enhanced-date-and-time-features"></a>增強型日期和時間功能的 SQLFetchScroll 支援  
 結果資料行值的日期/時間類型轉換中所述[從 SQL 轉換成 C](../native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md)。  
  
 如需詳細資訊，請參閱[日期和時間增強功能&#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlfetchscroll-support-for-large-clr-udts"></a>大型 CLR UDT 的 SQLFetchScroll 支援  
 **SQLFetchScroll**支援大型 CLR 使用者定義型別 (Udt)。 如需詳細資訊，請參閱[Large CLR User-Defined 類型&#40;ODBC&#41;](../native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLFetchScroll 函數](http://go.microsoft.com/fwlink/?LinkId=59343)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  