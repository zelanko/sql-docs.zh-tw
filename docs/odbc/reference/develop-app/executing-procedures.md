---
title: 執行程序 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ff234d1d8e099611c8718eac5ae3b584e926a2bd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63061966"
---
# <a name="executing-procedures"></a>執行程序
ODBC 定義標準逸出序列執行程序。 如需此順序和使用它的程式碼範例的語法，請參閱[程序呼叫](../../../odbc/reference/develop-app/procedure-calls.md)。  
  
 若要執行的程序，應用程式會執行下列動作：  
  
1.  設定任何參數的值。 如需詳細資訊，請參閱 <<c0> [ 陳述式參數](../../../odbc/reference/develop-app/statement-parameters.md)稍後這一節。  
  
2.  呼叫**SQLExecDirect**並將它傳遞為字串，包含執行程序的 SQL 陳述式。 此陳述式可以使用 ODBC 或 DBMS 專屬的語法; 所定義的逸出序列使用的 DBMS 特定語法的陳述式不具互通性。  
  
3.  當**SQLExecDirect**呼叫時，驅動程式：  
  
    -   擷取目前的參數值，並將它們轉換為必要。 如需詳細資訊，請參閱 <<c0> [ 陳述式參數](../../../odbc/reference/develop-app/statement-parameters.md)稍後這一節。  
  
    -   呼叫資料來源中的程序，並將它傳送的已轉換的參數值。 驅動程式如何呼叫程序是特定驅動程式。 比方說，它可能會修改 SQL 陳述式來使用資料來源的 SQL 文法，並提交執行時，此陳述式，或它可能會呼叫程序中直接使用 DBMS 的資料流通訊協定中定義的遠端程序呼叫 (RPC) 機制。  
  
    -   傳回的任何輸入/輸出或輸出參數的值或程序的傳回值，假設此程序成功。 處理所有其他結果 （資料列計數和結果集） 產生程序之後，可能無法使用這些值。 如果程序失敗，驅動程式會傳回任何錯誤。
