---
title: 交易支援 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], degree of support
ms.assetid: d56e1458-8da2-4d73-a777-09e045c30a33
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7b0e218f23ad720f8626c5b5e963038c194ae389
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="transaction-support"></a>交易支援
交易程度是支援的驅動程式定義。 ODBC 被設計來管理多個更新，其資料不需要在單一使用者或桌面資料庫上實作。 此外，某些支援交易的資料庫進行，只讓資料操作語言 (DML) 陳述式的 SQL。沒有限制或特殊交易語意有關使用資料定義語言 (DDL) 使用中交易時。 也就是可能對資料表的多個同時更新，但對變更的數目與定義的資料表在交易期間的交易支援。  
  
 應用程式會決定是否支援交易，指出是否 DDL 可以包含在交易中，而在交易中，包括 DDL，藉由呼叫的任何特殊效果**SQLGetInfo** SQL_TXN_CAPABLE 選項。 如需詳細資訊，請參閱[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函式描述。  
  
 如果驅動程式不支援交易，但應用程式有鎖定和解除鎖定資料 （使用 ODBC 以外的應用程式開發介面） 的功能，應用程式可以達到鎖定和解除鎖定資料錄的資料表所需的交易支援。 若要實作帳戶傳輸範例中，應用程式會鎖定這兩個帳戶的記錄、 複製目前的值、 借方的第一個帳戶，第二個帳戶的信用額度和解除鎖定記錄。 如果任何步驟失敗，應用程式會重設的帳戶使用的複本。  
  
 支援交易，甚至是資料來源可能無法支援一次在特定環境的多個交易。 應用程式呼叫**SQLGetInfo** SQL_MULTIPLE_ACTIVE_TXN 選項，以判斷資料來源是否可以支援同時使用中交易的相同環境中的多個連接上使用。 因為每個連線的一筆交易，這是只有興趣有多個連線到相同的資料來源的應用程式。
