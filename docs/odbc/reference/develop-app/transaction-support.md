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
ms.openlocfilehash: a0b5e33f94c5452a2062f7c18339f27c8da73fa9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68086060"
---
# <a name="transaction-support"></a>交易支援
交易的支援程度是驅動程式定義的。 ODBC 的設計目的是要在單一使用者或桌面資料庫上執行，而不需要管理其資料的多項更新。 此外，某些支援交易的資料庫，只會針對 SQL 的資料操作語言（DML）語句執行此動作;當交易在使用中時，有一些關於資料定義語言（DDL）用法的限制或特殊交易語義。 也就是說，可能會有多個對資料表的同時更新的交易支援，但不能在交易期間變更資料表的數目和定義。  
  
 應用程式會藉由使用 SQL_TXN_CAPABLE 選項呼叫**SQLGetInfo** ，判斷是否支援交易、是否可將 ddl 包含在交易中，以及在交易中包含 ddl 的任何特殊效果。 如需詳細資訊，請參閱[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函數描述。  
  
 如果驅動程式不支援交易，但應用程式有能力（使用 ODBC 以外的 API）來鎖定和解除鎖定資料，應用程式可以視需要鎖定和解除鎖定記錄和資料表，以達到交易支援。 若要執行帳戶傳輸範例，應用程式會鎖定這兩個帳戶的記錄、複製目前的值、支付第一個帳戶、取得第二個帳戶的點數，以及解除鎖定記錄。 如果有任何步驟失敗，應用程式會使用這些複本重設帳戶。  
  
 即使是支援交易的資料來源，也可能無法在特定環境中一次支援一個以上的交易。 應用程式會使用 SQL_MULTIPLE_ACTIVE_TXN 選項來呼叫**SQLGetInfo** ，以判斷資料來源是否可以在相同的環境中支援多個連接上同時使用的交易。 由於每個連接都有一個交易，因此只有對相同資料來源有多個連接的應用程式才會感興趣。
