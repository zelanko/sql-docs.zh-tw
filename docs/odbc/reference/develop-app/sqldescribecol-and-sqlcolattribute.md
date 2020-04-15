---
title: SQL描述科爾和 SQLCol 屬性 |微軟文件
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
ms.openlocfilehash: 8bd21010908473e4216a02a504b2de25578d5c84
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299758"
---
# <a name="sqldescribecol-and-sqlcolattribute"></a>SQLDescribeCol 和 SQLColAttribute
**SQLDescribeCol**和**SQLColAttribute**用於檢索結果集元數據。 這兩個函數之間的區別是**SQLDescribeCol**始終返回相同的五條資訊(列的名稱、數據類型、精度、縮放和空值),而**SQLColAttribute**返回應用程式請求的單個資訊段。 但是 **,SQLColAttribute**可以返回更豐富的元數據選擇,包括列的區分大小、顯示大小、高數據性和可搜索性。  
  
 許多應用程式,尤其是僅顯示數據的應用程式,只需要**SQLDescribeCol**返回的元數據。 對於這些應用程式,使用**SQLDescribeCol**比**SQLColAttribute**更快,因為資訊在單個調用中返回。 其他應用程式(尤其是更新數據的應用程式)需要**SQLColAttribute**傳回的其他元數據,因此可以使用這兩個函數。 此外 **,SQLColAttribute**支援特定於驅動程式的元數據;有關詳細資訊,請參閱[特定於驅動程式的資料類型、描述符類型、資訊類型、診斷類型和屬性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)。  
  
 應用程式可以在準備或執行語句后以及關閉結果集上的游標之前隨時檢索結果集元數據。 很少的應用程式在編寫語句后和執行語句之前需要結果集元數據。 如果可能,應用程式應等待檢索元數據,直到執行語句之後,因為某些數據源無法返回已準備的語句的元數據,並且在驅動程式中類比此功能通常是一個緩慢的過程。 例如,驅動程式可以通過將**SELECT**語句的**WHERE**子句替換為子句 WHERE 1 = **2**並執行結果語句來生成零行結果集。  
  
 從數據源檢索元數據通常成本高昂。 因此,驅動程式應緩存他們從伺服器檢索到的任何元數據,並按住它,只要結果集上的游標處於打開狀態。 此外,應用程式應僅請求他們絕對需要的元數據。
