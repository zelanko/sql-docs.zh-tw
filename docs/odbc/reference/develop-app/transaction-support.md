---
title: 交易支援 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], degree of support
ms.assetid: d56e1458-8da2-4d73-a777-09e045c30a33
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: be133079c1b6beffd484942eb9ae058c14dd5c1f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63306041"
---
# <a name="transaction-support"></a>交易支援
交易支援的程度是驅動程式定義。 ODBC 被設計來在單一使用者或桌面的資料庫具有不需要管理多個更新，其資料上實作。 此外，某些支援交易的資料庫進行只能在將的 SQL、 資料操作語言 (DML) 陳述式有限制或特殊的交易語意，有關使用資料定義語言 (DDL) 的使用中交易時。 也就是可能有多個同時更新資料表但未變更的數目和定義的資料表在交易期間的交易支援。  
  
 應用程式會決定是否支援交易，是否可以在交易中，而任何特殊效果，在交易中，包括 DDL，藉由呼叫包含 DDL **SQLGetInfo** SQL_TXN_CAPABLE 選項。 如需詳細資訊，請參閱 < [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函式描述。  
  
 如果驅動程式不支援交易，但應用程式有鎖定和解除鎖定資料的能力 （使用 ODBC 以外的 API），應用程式可以達到鎖定和解除鎖定的記錄和資料表所需的交易的支援。 若要實作帳戶移轉範例，應用程式會鎖定這兩個帳戶的記錄，複製目前的值、 借方的第一個帳戶、 點數第二個帳戶，並解除鎖定資料錄。 如果任何步驟失敗，應用程式會重設的帳戶使用的複本。  
  
 支援交易的平均資料來源可能無法支援一次在特定環境的多個交易。 應用程式會呼叫**SQLGetInfo** SQL_MULTIPLE_ACTIVE_TXN 選項，以決定是否為資料來源可以支援同時使用中交易的相同環境中的多個連接上使用。 因為每個連線的一筆交易，這是只需要有多個連線至相同的資料來源的應用程式。
