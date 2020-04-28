---
title: 使用 SQLBulkOperations 插入資料列 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBulkOperations function [ODBC], inserting rows
- data updates [ODBC], SQLBulkOperations
- updating data [ODBC], SQLBulkOperations
ms.assetid: ed585ea7-4d56-4df9-8dc3-53ca82382450
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a6fa384292f02026b8390aa92525144dce6f549b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300108"
---
# <a name="inserting-rows-with-sqlbulkoperations"></a>使用 SQLBulkOperations 插入資料列
使用**SQLBulkOperations**插入資料類似于以**SQLBulkOperations**更新資料，因為它會使用系結應用程式緩衝區中的資料。  
  
 因此，新資料列中的每個資料行都有一個值，而所有系結資料行的長度/指標值為 SQL_COLUMN_IGNORE 且所有未系結的資料行都必須接受 Null 值或具有預設值。  
  
 若要使用**SQLBulkOperations**插入資料列，應用程式會執行下列動作：  
  
1.  將 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性設定為要插入的資料列數目，並將新的資料值放在系結的應用程式緩衝區中。 如需有關如何使用**SQLBulkOperations**傳送長資料的詳細資訊，請參閱[冗長資料和 SQLSetPos 和 SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)。  
  
2.  視需要設定每個資料行的長度/指標緩衝區中的值。 這是系結至字串緩衝區的 SQL_NTS 資料行的位元組長度、系結至二進位緩衝區之資料行的位元組長度，以及要設定為 Null 的任何資料行 SQL_Null_DATA。 應用程式會在要設定為預設值的資料行（如果存在的話）或 Null （如果沒有的話）中，設定要 SQL_COLUMN_IGNORE 的長度/指標緩衝區的值。  
  
3.  呼叫**SQLBulkOperations** ，並將*Operation*引數設定為 SQL_ADD。  
  
 在**SQLBulkOperations**傳回之後，目前的資料列就不會變更。 如果書簽資料行（資料行0）已系結， **SQLBulkOperations**會在系結至該資料行的資料列集緩衝區中，傳回插入資料列的書簽。
