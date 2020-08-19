---
description: 長資料和 SQLSetPos 與 SQLBulkOperations
title: Long Data 和 SQLSetPos 和 SQLBulkOperations |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- long data [ODBC]
- SQLSetPos function [ODBC], long data and SQLBulkOperations
- data updates [ODBC], long data
- updating data [ODBC], long data
- SQLBulkOperations function [ODBC], long data
ms.assetid: e2fdf842-5e4c-46ca-bb21-4625c3324f28
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 12bc0299df58bf85272445773a8f33a872c39ef2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429270"
---
# <a name="long-data-and-sqlsetpos-and-sqlbulkoperations"></a>長資料和 SQLSetPos 與 SQLBulkOperations
如同 SQL 語句中的參數，在使用 **SQLBulkOperations** 或 **SQLSetPos** 來更新資料列時，或使用 **SQLBulkOperations**插入資料列時，可能會傳送 long 資料。 資料會在元件中傳送，並有多個 **SQLPutData**呼叫。 在執行時間傳送資料的資料行稱為「 *資料執行中資料行*」。  
  
> [!NOTE]  
>  應用程式實際上可以使用 **SQLPutData**在執行時間傳送任何類型的資料，雖然只有字元和二進位資料可以在部分中傳送。 但是，如果資料夠小而足以容納在單一緩衝區中，則通常沒有理由使用 **SQLPutData**。 系結緩衝區更容易，並讓驅動程式從緩衝區中取出資料。  
  
 因為 long data 資料行通常未系結，所以在呼叫 **SQLBulkOperations** 或 **SQLSetPos** 之前，應用程式必須系結資料行，然後在呼叫 **SQLBulkOperations** 或 **SQLSetPos**之後解除系結。 必須系結資料行，因為 **SQLBulkOperations** 或 **SQLSetPos** 只會在系結資料行上運作，而且必須解除系結，才能使用 **SQLGetData** 來從資料行中取出資料。  
  
 若要在執行時間傳送資料，應用程式會執行下列動作：  
  
1.  將32位值放在資料列集緩衝區中，而不是資料值。 此值稍後會傳回給應用程式，因此應用程式應該將它設定為有意義的值，例如資料行的數目或包含資料之檔案的控制碼。  
  
2.  將長度/指標緩衝區中的值設定為 SQL_LEN_DATA_AT_EXEC (*長度*) 宏的結果。 此值會向驅動程式指出參數的資料將會與 **SQLPutData**一起傳送。 將長資料傳送至資料來源時，會使用 *長度* 值，該資料來源必須知道將傳送多少位元組的 long 資料，才能預先配置空間。 若要判斷資料來源是否需要此值，應用程式會使用 SQL_NEED_LONG_DATA_LEN 選項來呼叫 **SQLGetInfo** 。 所有驅動程式都必須支援此宏;如果資料來源不需要位元組長度，驅動程式可以忽略它。  
  
3.  呼叫 **SQLBulkOperations** 或 **SQLSetPos**。 驅動程式會發現長度/指標緩衝區包含 SQL_LEN_DATA_AT_EXEC (*長度*) 宏的結果，並傳回 SQL_NEED_DATA 做為函數的傳回值。  
  
4.  呼叫 **SQLParamData** 以回應 SQL_NEED_DATA 傳回值。 如果需要傳送長的資料， **SQLParamData** 會傳回 SQL_NEED_DATA。 在 *ValuePtrPtr* 引數所指向的緩衝區中，驅動程式會傳回應用程式放在資料列集緩衝區中的唯一值。 如果有多個資料執行中資料行，應用程式會使用這個值來決定要傳送資料的資料行;不需要驅動程式，就能以任何特定順序要求資料執行中資料行的資料。  
  
5.  呼叫 **SQLPutData** 以將資料行資料傳送至驅動程式。 如果資料行資料無法容納在單一緩衝區中（通常是使用 long 資料的情況），則應用程式會重複呼叫 **SQLPutData** ，以將資料傳送至部分;它是由驅動程式和資料來源所組成，以重組資料。 如果應用程式傳遞以 null 終止的字串資料，則驅動程式或資料來源必須在重新組合過程中移除 null 終止字元。  
  
6.  再次呼叫 **SQLParamData** ，表示它已傳送資料行的所有資料。 如果有任何未傳送資料的資料執行中資料行，驅動程式會傳回 SQL_NEED_DATA 以及下一個資料執行中資料行的唯一值;應用程式會返回步驟5。 如果已傳送所有資料執行中資料行的資料，資料列的資料就會傳送到資料來源。 然後， **SQLParamData**會傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，而且可以傳回**SQLBulkOperations**或**SQLSETPOS**可以傳回的任何 SQLSTATE。  
  
 在 **SQLBulkOperations** 或 **SQLSetPos** 傳回 SQL_NEED_DATA，且在完全傳送最後一個資料執行中資料行的資料之前，語句會處於 [需要資料] 狀態。 在此狀態下，應用程式只能呼叫 **SQLPutData**、 **SQLParamData**、 **SQLCancel**、 **SQLGetDiagField**或 **SQLGetDiagRec**;所有其他函式會傳回 SQLSTATE HY010 (函數順序錯誤) 。 呼叫 **SQLCancel** 會取消語句的執行，並將其傳回至先前的狀態。 如需詳細資訊，請參閱 [附錄 B： ODBC 狀態轉換資料表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。
