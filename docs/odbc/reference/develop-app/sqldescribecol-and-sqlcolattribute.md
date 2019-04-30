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
manager: craigg
ms.openlocfilehash: e569e51540cbaa5612b158abdacac5faae77f940
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63149035"
---
# <a name="sqldescribecol-and-sqlcolattribute"></a>SQLDescribeCol 和 SQLColAttribute
**SQLDescribeCol**並**SQLColAttribute**用來擷取結果集中繼資料。 這兩個函數之間的差異在於**SQLDescribeCol**一律會傳回相同的五項資訊 （資料行的名稱、 資料類型、 有效位數、 小數位數和 null 屬性），同時**SQLColAttribute**會傳回單一的應用程式要求的資訊。 不過， **SQLColAttribute**可以傳回更豐富的中繼資料，包括資料行的區分大小寫的選取項目，顯示大小、 可更新性和搜尋能力。  
  
 許多應用程式，特別是只會顯示資料，需要所傳回的中繼資料**SQLDescribeCol**。 對於這些應用程式中，速度會使用**SQLDescribeCol**比**SQLColAttribute**因為單一呼叫中傳回的資訊。 其他應用程式，特別是更新資料時，需要所傳回的其他中繼資料**SQLColAttribute** ，因此使用這兩個函式。 颾魤 ㄛ **SQLColAttribute**支援的驅動程式專屬的中繼資料; 如需詳細資訊，請參閱[驅動程式專屬資料型別、 描述項類型、 資訊類型、 診斷類型和屬性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)。  
  
 在任何時間，並已備妥或執行陳述式之前的資料指標的結果集就會關閉之後，應用程式可以擷取結果集中繼資料。 極少數的應用程式需要在準備陳述式之後，會在執行之前，結果集中繼資料。 可能的話，應用程式應該等待擷取中繼資料，直到之後執行的陳述式，因為某些資料來源不能傳回的已備妥的陳述式中繼資料，並模擬驅動程式中的這項功能通常是緩慢的程序。 比方說，驅動程式可能會產生零資料列結果集，藉由取代**何處**子句**選取**with 子句的陳述式**WHERE 1 = 2**和執行產生的陳述式。  
  
 中繼資料通常很昂貴，從資料來源擷取的。 因為這個緣故，驅動程式應該快取它們從伺服器擷取和保存的只要將游標放結果設定為開啟狀態的任何中繼資料。 此外，應用程式應該要求絕對需要的中繼資料。
