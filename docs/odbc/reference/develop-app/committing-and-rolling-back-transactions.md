---
title: 認可及回復交易 |Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68083313"
---
# <a name="committing-and-rolling-back-transactions"></a>認可及回復交易
若要認可或回復交易在手動認可模式下，應用程式會呼叫**SQLEndTran**。 通常支援交易的 Dbms 的驅動程式來實作此函式執行**認可**或是**ROLLBACK**陳述式。 驅動程式管理員不會呼叫**SQLEndTran**時連接處於自動認可模式，它只會傳回 SQL_SUCCESS，即使應用程式會嘗試回復交易。 因為不支援交易的 Dbms 的驅動程式永遠會在自動認可模式下，它們可以實作**SQLEndTran**傳回 SQL_SUCCESS，而不會執行任何動作，或未實作。  
  
> [!NOTE]  
>  應用程式不應該認可或回復執行的交易**認可**或是**ROLLBACK**陳述式與**SQLExecute**或**SQLExecDirect**. 執行此動作的作用是未定義。 可能的問題包括驅動程式不會再了解當交易正在作用中並無法對資料來源不支援交易，這些陳述式。 這些應用程式應該呼叫**SQLEndTran**改。  
  
 如果應用程式通過的環境控制代碼**SQLEndTran**但是不會傳遞連接控制代碼，驅動程式管理員會在概念上呼叫**SQLEndTran**搭配每個驅動程式的環境控制代碼，在環境中有一或多個作用中連線。 驅動程式則會認可在環境中的每個連接上的交易。 不過，務必要了解，驅動程式和驅動程式管理員都不會執行兩階段交易認可中的環境; 的連線這只是要程式設計同時呼叫**SQLEndTran**在環境中的所有連線。  
  
 (A*兩階段交易認可*通常用來認可會分散到多個資料來源的交易。 在其第一個階段中，資料來源會輪詢對於是否能認可交易的一部分。 在第二個階段中，實際上是在所有的資料來源上認可交易。 如果任何資料來源中的第一個階段回覆它們無法認可交易，方法是，第二個階段不會發生。）
