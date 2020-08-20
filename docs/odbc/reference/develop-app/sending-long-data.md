---
description: 傳送長資料
title: 傳送長資料 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- long data [ODBC]
- sending long data [ODBC]
ms.assetid: ea989084-a8e6-4737-892e-9ec99dd49caf
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f6a0ec1a7e8dc703d3e7a3ed5332d20e6539eafe
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476460"
---
# <a name="sending-long-data"></a>傳送長資料
Dbms 將 *長資料* 定義為特定大小的任何字元或二進位資料，例如254個字元。 可能無法將長資料的整個專案儲存在記憶體中，例如當專案代表長文字檔或點陣圖時。 由於這類資料無法儲存在單一緩衝區中，因此當執行語句時，資料來源會將該資料傳送至具有 **SQLPutData** 元件的驅動程式。 在執行時間傳送資料的參數稱為「 *資料執行中參數*」。  
  
> [!NOTE]  
>  應用程式實際上可以使用 **SQLPutData**在執行時間傳送任何類型的資料，雖然只有字元和二進位資料可以在部分中傳送。 但是，如果資料夠小而足以容納在單一緩衝區中，則通常沒有理由使用 **SQLPutData**。 系結緩衝區更容易，並讓驅動程式從緩衝區中取出資料。  
  
 若要在執行時間傳送資料，應用程式會執行下列動作：  
  
1.  傳遞32位的值，此值會識別**SQLBindParameter**中*ParameterValuePtr*引數的參數，而不是傳遞緩衝區的位址。 驅動程式不會分析此值。 稍後會將它傳回給應用程式，所以它應該會對應用程式造成一些意義。 例如，它可能是參數的數目或包含資料之檔案的控制碼。  
  
2.  在**SQLBindParameter**的*StrLen_or_IndPtr*引數中傳遞長度/指標緩衝區的位址。  
  
3.  儲存長度/指標緩衝區中 SQL_LEN_DATA_AT_EXEC (*長度*) 宏的 SQL_DATA_AT_EXEC 或結果。 這兩個值都會向驅動程式指出參數的資料將會與 **SQLPutData**一起傳送。 將長資料傳送到資料來源時，會使用 SQL_LEN_DATA_AT_EXEC (*長度*) ，而此資料來源必須知道將傳送多少位元組的 long 資料，才能預先配置空間。 為了判斷資料來源是否需要此值，應用程式會使用 SQL_NEED_LONG_DATA_LEN 選項來呼叫 **SQLGetInfo** 。 所有驅動程式都必須支援此宏;如果資料來源不需要位元組長度，驅動程式可以忽略它。  
  
4.  呼叫 **SQLExecute** 或 **SQLExecDirect**。 驅動程式會發現長度/指標緩衝區包含 SQL_DATA_AT_EXEC 的值，或是 SQL_LEN_DATA_AT_EXEC (*長度*) 宏的結果，並傳回 SQL_NEED_DATA 做為函式的傳回值。  
  
5.  呼叫 **SQLParamData** 以回應 SQL_NEED_DATA 傳回值。 如果需要傳送長的資料， **SQLParamData** 會傳回 SQL_NEED_DATA。 在 *ValuePtrPtr* 引數所指向的緩衝區中，驅動程式會傳回識別資料執行中參數的值。 如果有多個資料執行中參數，應用程式必須使用此值來決定要傳送資料的參數;驅動程式不需要以任何特定順序要求資料執行中參數的資料。  
  
6.  呼叫 **SQLPutData** 將參數資料傳送至驅動程式。 如果參數資料不符合單一緩衝區（通常是使用 long 資料的情況），則應用程式會重複呼叫 **SQLPutData** ，以將資料傳送至部分;它是由驅動程式和資料來源所組成，以重組資料。 如果應用程式傳遞以 null 終止的字串資料，則驅動程式或資料來源必須在重新組合過程中移除 null 終止字元。  
  
7.  再次呼叫 **SQLParamData** ，表示它已傳送參數的所有資料。 如果有任何未傳送資料的資料執行中參數，驅動程式會傳回 SQL_NEED_DATA 以及可識別下一個參數的值;應用程式會回到步驟6。 如果已傳送所有資料執行中參數的資料，就會執行語句。 **SQLParamData** 會傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，而且可以傳回 **SQLExecute** 或 **SQLExecDirect** 可傳回的任何傳回值或診斷。  
  
 在 **SQLExecute** 或 **SQLExecDirect** 傳回 SQL_NEED_DATA，且在完全傳送最後一個資料執行中參數的資料之前，語句會處於 [需要資料] 狀態。 當語句在需要資料狀態時，應用程式只能呼叫 **SQLPutData**、 **SQLParamData**、 **SQLCancel**、 **SQLGetDiagField**或 **SQLGetDiagRec**;所有其他函式會傳回 SQLSTATE HY010 (函數順序錯誤) 。 呼叫 **SQLCancel** 會取消語句的執行，並將其傳回至先前的狀態。 如需詳細資訊，請參閱 [附錄 B： ODBC 狀態轉換資料表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
 如需在執行時間傳送資料的範例，請參閱 [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md) 函數描述。
