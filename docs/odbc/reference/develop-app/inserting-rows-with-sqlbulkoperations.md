---
description: 使用 SQLBulkOperations 插入資料列
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
ms.openlocfilehash: 36f04a393d2053389f823c33a55050f24dd87020
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424630"
---
# <a name="inserting-rows-with-sqlbulkoperations"></a>使用 SQLBulkOperations 插入資料列
使用 **SQLBulkOperations** 插入資料類似于使用 **SQLBulkOperations** 來更新資料，因為它會使用來自系結應用程式緩衝區的資料。  
  
 如此一來，新資料列中的每個資料行都有一個值，且長度/指標值為 SQL_COLUMN_IGNORE 且所有未系結資料行的所有系結資料行都必須接受 Null 值或具有預設值。  
  
 若要使用 **SQLBulkOperations**插入資料列，應用程式會執行下列動作：  
  
1.  將 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性設定為要插入的資料列數目，並將新的資料值放在系結的應用程式緩衝區中。 如需有關如何使用 **SQLBulkOperations**傳送長資料的詳細資訊，請參閱 [Long data And SQLSetPos and SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)。  
  
2.  視需要設定每個資料行的長度/指標緩衝區中的值。 這是系結至字串緩衝區之資料行的資料或 SQL_NTS 的位元組長度、系結至二進位緩衝區的資料行之資料的位元組長度，以及要設定為 Null 之任何資料行的 SQL_Null_DATA。 應用程式會將這些資料行的長度/指標緩衝區中的值設定為其預設 (（如果有的話）) 或 Null (如果沒有) SQL_COLUMN_IGNORE 的話）。  
  
3.  呼叫 **SQLBulkOperations** ，並將 *Operation* 引數設定為 SQL_ADD。  
  
 在 **SQLBulkOperations** 傳回之後，目前的資料列就不會變更。 如果系結 (資料行 0) 的書簽資料行， **SQLBulkOperations** 會傳回系結至該資料行之資料列集緩衝區中插入之資料列的書簽。
