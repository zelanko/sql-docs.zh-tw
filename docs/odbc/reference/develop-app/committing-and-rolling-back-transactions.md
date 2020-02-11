---
title: 認可和回復交易 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- rolling back transactions [ODBC]
- committing transactions [ODBC]
- transactions [ODBC], rolling back
- transactions [ODBC], committing
ms.assetid: 800f2c1a-6f79-4ed1-830b-aa1a62ff5165
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c7c028ca7e89378e959b11f59cad4119cef5086a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68083313"
---
# <a name="committing-and-rolling-back-transactions"></a>認可及回復交易
若要在手動認可模式中認可或回復交易，應用程式會呼叫**SQLEndTran**。 支援交易之 Dbms 的驅動程式通常會藉由執行**COMMIT**或**ROLLBACK**語句來執行此函數。 當連接處於自動認可模式時，驅動程式管理員不會呼叫**SQLEndTran** ;它只會傳回 SQL_SUCCESS，即使應用程式嘗試復原交易也一樣。 由於不支援交易的 Dbms 驅動程式一律處於自動認可模式，因此可以執行**SQLEndTran**以傳回 SQL_SUCCESS，而不需要執行任何動作或完全不進行執行。  
  
> [!NOTE]  
>  應用程式不應該藉由使用**SQLExecute**或**SQLExecDirect**來執行**commit**或**ROLLBACK**語句，來認可或回復交易。 執行此動作的效果未定義。 可能的問題包括驅動程式已不再知道交易何時作用中，而且這些語句會針對不支援交易的資料來源而失敗。 這些應用程式應該改為呼叫**SQLEndTran** 。  
  
 如果應用程式將環境控制碼傳遞至**SQLEndTran** ，但未傳遞連接控制碼，則驅動程式管理員在概念上會針對每個在環境中具有一或多個作用中連接的驅動程式，以環境控制碼呼叫**SQLEndTran** 。 然後，驅動程式會在環境中的每個連接上認可交易。 不過，請務必瞭解驅動程式或驅動程式管理員都不會在環境中的連線上執行兩階段認可;這只是一種程式設計方便，可同時為環境中的所有連接呼叫**SQLEndTran** 。  
  
 （*兩階段認可*通常用來認可分散到多個資料來源的交易。 在第一個階段中，資料來源會輪詢，以判斷它們是否可以認可交易的一部分。 在第二個階段中，交易實際上是在所有資料來源上進行認可。 如果任何資料來源在第一個階段中回復，而無法認可交易，則不會發生第二個階段。）
