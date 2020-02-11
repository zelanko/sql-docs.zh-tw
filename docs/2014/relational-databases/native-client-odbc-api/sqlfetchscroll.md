---
title: SQLFetchScroll |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLFetchScroll function
ms.assetid: 524a3985-a08d-4445-99e0-bb551a666615
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3c9614a71c0015d17178a57d33c5fd0d9b62433c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63154681"
---
# <a name="sqlfetchscroll"></a>SQLFetchScroll
  **SQLFetchScroll**會將一個資料列集傳回給應用程式。 資料列集的大小是使用[SQLSetStmtAttr](sqlsetstmtattr.md)設定的。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驅動程式支援所有定義的提取指示（例如，SQL_FETCH_RELATIVE），但有下列限制：  
  
-   如果有針對陳述式而定義順向資料指標，則需要 SQL_FETCH_NEXT，而且以任何其他格式嘗試提取會導致錯誤傳回。  
  
-   僅針對靜態和索引鍵集導向的資料指標支援 SQL_FETCH_BOOKMARK。  
  
## <a name="sqlfetchscroll-support-for-enhanced-date-and-time-features"></a>增強型日期和時間功能的 SQLFetchScroll 支援  
 日期/時間類型的結果資料行值會轉換，如[從 SQL 轉換為 C](../native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md)中所述。  
  
 如需詳細資訊，請參閱[ODBC&#41;&#40;的日期和時間改善](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlfetchscroll-support-for-large-clr-udts"></a>大型 CLR UDT 的 SQLFetchScroll 支援  
 **SQLFetchScroll**支援大型 CLR 使用者定義型別（udt）。 如需詳細資訊，請參閱[&#40;ODBC&#41;的大型 CLR 使用者定義類型](../native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLFetchScroll 函式](https://go.microsoft.com/fwlink/?LinkId=59343)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  
