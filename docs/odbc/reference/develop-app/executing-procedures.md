---
title: 執行程序 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], procedures
- procedures [ODBC], executing
ms.assetid: a75e497a-4661-438a-a10e-f598c65f81be
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d61929c1d2afb756be5157f3378ff0fe6b4d7e95
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32910773"
---
# <a name="executing-procedures"></a>執行程序
ODBC 定義的標準逸出序列執行程序。 如需此順序和使用它的程式碼範例的語法，請參閱[程序呼叫](../../../odbc/reference/develop-app/procedure-calls.md)。  
  
 若要執行的程序，應用程式會執行下列動作：  
  
1.  設定任何參數的值。 如需詳細資訊，請參閱[陳述式參數](../../../odbc/reference/develop-app/statement-parameters.md)稍後這一節。  
  
2.  呼叫**SQLExecDirect**並將其傳遞字串，包含執行程序的 SQL 陳述式。 這個陳述式可以使用 ODBC 或 DBMS 特定語法; 所定義的逸出序列使用 DBMS 特定語法的陳述式並不互通。  
  
3.  當**SQLExecDirect**呼叫時，驅動程式：  
  
    -   擷取目前的參數值，並視需要進行轉換。 如需詳細資訊，請參閱[陳述式參數](../../../odbc/reference/develop-app/statement-parameters.md)稍後這一節。  
  
    -   呼叫資料來源中的程序，並將它傳送的已轉換的參數值。 驅動程式呼叫程序的方式是驅動程式專屬功能。 例如，它可能會修改 SQL 陳述式來使用資料來源的 SQL 文法和提交此陳述式執行，或它可能會呼叫程序中直接使用 DBMS 的資料流通訊協定中定義的遠端程序呼叫 (RPC) 機制。  
  
    -   傳回任何輸出或輸出參數的值或程序的傳回值，假設此程序成功。 處理所有其他結果 （資料列計數和結果集） 產生程序之後，可能無法後才可以使用這些值。 如果程序失敗，驅動程式會傳回任何錯誤。
