---
description: 認可及回復交易
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b84be4d2734d9485748351c99ff2675bf3b54213
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424840"
---
# <a name="committing-and-rolling-back-transactions"></a>認可及回復交易
若要在手動認可模式下認可或復原交易，應用程式會呼叫 **SQLEndTran**。 支援交易的 Dbms 的驅動程式通常會藉由執行 **COMMIT** 或 **ROLLBACK** 語句來執行此函數。 當連接處於自動認可模式時，驅動程式管理員不會呼叫 **SQLEndTran** ;即使應用程式嘗試回復交易，它只會傳回 SQL_SUCCESS。 因為 Dbms 的驅動程式一律處於自動認可模式，所以它們可以執行 **SQLEndTran** 來傳回 SQL_SUCCESS 而不需要執行任何動作，或完全不執行任何動作。  
  
> [!NOTE]  
>  應用程式不應使用**SQLExecute**或**SQLExecDirect**執行**commit**或**ROLLBACK**語句，來認可或回復交易。 執行這項操作的效果是未定義的。 可能的問題包括驅動程式不再知道交易何時處於作用中狀態，而且這些語句無法針對不支援交易的資料來源。 這些應用程式應該改為呼叫 **SQLEndTran** 。  
  
 如果應用程式將環境控制碼傳遞至 **SQLEndTran** ，但未通過連線控制碼，則驅動程式管理員會在概念上針對環境中有一或多個作用中連線的每個驅動程式，使用環境控制碼來呼叫 **SQLEndTran** 。 然後，驅動程式會認可環境中每個連接的交易。 不過，請務必瞭解驅動程式和驅動程式管理員都不會在環境中的連線上執行兩階段認可;這只是針對環境中的所有連接同時呼叫 **SQLEndTran** 的程式設計便利性。  
  
  (*兩階段認可* 通常用來認可分散至多個資料來源的交易。 在第一個階段中，會將資料來源輪詢為是否可以認可交易的部分。 在第二個階段中，交易實際上是在所有資料來源上進行認可。 如果任何資料來源在無法認可交易的第一個階段回復，則不會發生第二個階段。 ) 
