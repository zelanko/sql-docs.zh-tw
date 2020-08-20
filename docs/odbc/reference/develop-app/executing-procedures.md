---
description: 執行程序
title: 執行程式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], procedures
- procedures [ODBC], executing
ms.assetid: a75e497a-4661-438a-a10e-f598c65f81be
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e4a5f790a0e79e313924e9408f9338483931691c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499909"
---
# <a name="executing-procedures"></a>執行程序
ODBC 會定義執行程式的標準 escape 順序。 如需此序列的語法和使用它的程式碼範例，請參閱 [程序呼叫](../../../odbc/reference/develop-app/procedure-calls.md)。  
  
 若要執行程式，應用程式會執行下列動作：  
  
1.  設定任何參數的值。 如需詳細資訊，請參閱本節稍後的 [語句參數](../../../odbc/reference/develop-app/statement-parameters.md)。  
  
2.  呼叫 **SQLExecDirect** ，並將包含執行程式之 SQL 語句的字串傳遞給它。 這個語句可以使用 ODBC 或 DBMS 特定語法所定義的 escape 序列;使用 DBMS 特定語法的語句無法互通。  
  
3.  當呼叫 **SQLExecDirect** 時，驅動程式：  
  
    -   抓取目前的參數值，並視需要進行轉換。 如需詳細資訊，請參閱本節稍後的 [語句參數](../../../odbc/reference/develop-app/statement-parameters.md)。  
  
    -   呼叫資料來源中的程式，並將轉換後的參數值傳送給它。 驅動程式如何呼叫程式是驅動程式特定的。 例如，它可能會修改 SQL 語句，以使用資料來源的 SQL 文法並提交此語句來執行，或者，它可能會使用遠端程序呼叫直接呼叫程式， (在 DBMS 的資料流程通訊協定中定義的 RPC) 機制。  
  
    -   傳回任何輸入/輸出或輸出參數的值或程式傳回值（假設程式成功）。 這些值必須等到所有其他結果都 (資料列計數，且已處理常式所產生) 的結果集之後，才可以使用這些值。 如果程式失敗，驅動程式會傳回任何錯誤。
