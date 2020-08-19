---
description: SQLDescribeCol 和 SQLColAttribute
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2de375ea207e8e393fa36c9795ebf0e3ca5f428b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424500"
---
# <a name="sqldescribecol-and-sqlcolattribute"></a>SQLDescribeCol 和 SQLColAttribute
**SQLDescribeCol** 和 **SQLColAttribute** 可用來取出結果集中繼資料。 這兩個函式之間的差異在於， **SQLDescribeCol** 一律會傳回相同的五項資訊 (資料行的名稱、資料類型、精確度、小數位數和 null 屬性) ，而 **SQLColAttribute** 會傳回應用程式所要求的單一資訊片段。 不過， **SQLColAttribute** 可以傳回更豐富的中繼資料選取範圍，包括資料行的區分大小寫、顯示大小、可更新性和搜尋能力。  
  
 許多應用程式（特別是只顯示資料的應用程式）只需要 **SQLDescribeCol**傳回的中繼資料。 針對這些應用程式，使用 **SQLDescribeCol** 比 **SQLColAttribute** 更快，因為這項資訊會在單一呼叫中傳回。 其他應用程式（特別是更新資料的應用程式）需要 **SQLColAttribute** 傳回的額外中繼資料，因此請使用這兩個函數。 此外， **SQLColAttribute** 還支援驅動程式專用的中繼資料;如需詳細資訊，請參閱 [驅動程式特定的資料類型、描述項類型、資訊類型、診斷類型與屬性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)。  
  
 應用程式可以在語句已備妥或執行之後，以及資料指標在結果集上關閉之前，隨時取得結果集中繼資料。 很少的應用程式在完成語句之後和執行之前都需要結果集中繼資料。 如果可能的話，應用程式應該等候取得中繼資料，直到執行語句為止，因為某些資料來源無法傳回備妥語句的中繼資料，以及在驅動程式中模擬這項功能通常是緩慢的進程。 例如，驅動程式可能會藉由以**1 = 2**的子句取代**SELECT**語句的**WHERE**子句，並執行產生的語句，來產生零資料列的結果集。  
  
 從資料來源取出中繼資料通常很昂貴。 因此，只要在結果集上開啟資料指標，驅動程式就應該快取從伺服器取出的任何中繼資料，並保留它。 此外，應用程式應該只要求他們絕對需要的中繼資料。
