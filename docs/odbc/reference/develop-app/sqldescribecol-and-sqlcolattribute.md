---
title: SQLDescribeCol 和 SQLColAttribute |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLColAttribute function [ODBC], and SQLDescribeCol
- SQLDescribeCol function [ODBC], and SQLColAttribute
- result sets [ODBC], metadata
- retrieving result set meta data [ODBC]
- metadata [ODBC], result set
ms.assetid: c2ca442c-03a8-4e0f-9e67-b300bb15962f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d602368475c6f1326cc615453116e898b1c1892f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107437"
---
# <a name="sqldescribecol-and-sqlcolattribute"></a>SQLDescribeCol 和 SQLColAttribute
**SQLDescribeCol**和**SQLColAttribute**是用來捕獲結果集中繼資料。 這兩個函式的差異在於， **SQLDescribeCol**一律會傳回相同的五項資訊（資料行名稱、資料類型、有效位數、小數位數和 null 屬性），而**SQLColAttribute**會傳回應用程式所要求的單一資訊片段。 不過， **SQLColAttribute**可以傳回更豐富的中繼資料選取範圍，包括資料行的區分大小寫、顯示大小、可更新性和搜尋能力。  
  
 許多應用程式（特別是只顯示資料的應用程式）只需要**SQLDescribeCol**所傳回的中繼資料。 對於這些應用程式而言，使用**SQLDescribeCol**比**SQLColAttribute**更快，因為會在單一呼叫中傳回信息。 其他應用程式（特別是更新資料的應用程式）需要**SQLColAttribute**所傳回的其他中繼資料，因此會使用這兩個函數。 此外， **SQLColAttribute**支援驅動程式特定的中繼資料;如需詳細資訊，請參閱[驅動程式特有的資料類型、描述項類型、資訊類型、診斷類型和屬性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)。  
  
 應用程式可以在準備或執行語句之後，以及在關閉結果集的資料指標之前，隨時取得結果集中繼資料。 非常少的應用程式在準備好和執行語句之後，會需要結果集中繼資料。 可能的話，應用程式應該等到語句執行後才抓取中繼資料，因為有些資料來源無法傳回備妥之語句的中繼資料，而且在驅動程式中模擬這項功能通常是緩慢的進程。 例如，驅動程式可能會產生零資料列的結果集，方法是以子句取代**SELECT**語句的**Where**子句，**其中 1 = 2**並執行產生的語句。  
  
 從資料來源抓取中繼資料通常相當耗費資源。 因此，驅動程式應該快取從伺服器抓取的任何中繼資料，只要結果集上的游標開啟，就會保留它。 此外，應用程式應該只要求其絕對需要的中繼資料。
