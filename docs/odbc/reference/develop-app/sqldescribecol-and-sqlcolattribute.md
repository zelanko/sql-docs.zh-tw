---
title: "SQLDescribeCol 和 SQLColAttribute |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLColAttribute function [ODBC], and SQLDescribeCol
- SQLDescribeCol function [ODBC], and SQLColAttribute
- result sets [ODBC], metadata
- retrieving result set meta data [ODBC]
- metadata [ODBC], result set
ms.assetid: c2ca442c-03a8-4e0f-9e67-b300bb15962f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9a80ccf6ed695433a109770a567f50d100fd3a33
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqldescribecol-and-sqlcolattribute"></a>SQLDescribeCol 和 SQLColAttribute
**SQLDescribeCol**和**SQLColAttribute**用來擷取結果集中繼資料。 這兩個函數之間的差異在於**SQLDescribeCol**一律會傳回相同的五項時的資訊 （資料行的名稱、 資料類型、 有效位數、 小數位數和 null 屬性）， **SQLColAttribute**傳回單一的應用程式要求的資訊。 不過， **SQLColAttribute**可以傳回更豐富的選取範圍的中繼資料，包括資料行的區分大小寫，顯示大小、 可更新性，以及搜尋能力。  
  
 許多應用程式，特別是只會顯示資料，需要所傳回的中繼資料**SQLDescribeCol**。 對於這些應用程式，速度會使用**SQLDescribeCol**比**SQLColAttribute**因為單一呼叫中傳回的資訊。 其他應用程式，特別是更新資料時，需要所傳回的其他中繼資料**SQLColAttribute** ，因此使用這兩個函數。 此外， **SQLColAttribute**支援驅動程式專屬的中繼資料; 如需詳細資訊，請參閱[驅動程式特定資料類型，描述元類型、 資訊類型、 診斷的型別，以及屬性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)。  
  
 應用程式可以在任何時間之後，尚未準備或執行陳述式集就會關閉資料指標結果上方，則之前擷取結果集中繼資料。 極少數的應用程式需要在準備陳述式之後，會在執行之前，結果集中繼資料。 可能的話，應該等候應用程式擷取中繼資料之前，執行陳述式，因為某些資料來源無法傳回已備妥的陳述式的中繼資料，並模擬驅動程式中的這項功能通常是緩慢的程序之後。 例如，驅動程式可能會產生零資料列結果集所取代**其中**子句**選取**with 子句的陳述式**WHERE 1 = 2**和執行產生的陳述式。  
  
 中繼資料通常是高度耗費資源，來擷取資料來源。 因為這個緣故，驅動程式應該快取它們從伺服器擷取和保存的只要設定結果上方，則資料指標是開啟的任何中繼資料。 此外，應用程式應該要求一定需要的中繼資料。

