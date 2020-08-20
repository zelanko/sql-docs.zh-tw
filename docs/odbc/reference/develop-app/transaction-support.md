---
description: 異動支援
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0218941606752ccd93c7bc9bdfe31096682c6d87
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476327"
---
# <a name="transaction-support"></a>異動支援
交易的支援程度為驅動程式定義。 ODBC 是設計來在單一使用者或桌面資料庫上執行，而不需要管理其資料的多個更新。 此外，某些支援交易的資料庫只會針對資料操作語言 (SQL 的 DML) 語句;當交易在使用中時，有關使用資料定義語言 (DDL) 有一些限制或特殊的交易語義。 也就是說，對資料表的多個同時更新可能會有交易支援，但不能在交易期間變更資料表的數目和定義。  
  
 應用程式會藉由使用 SQL_TXN_CAPABLE 選項來呼叫 **SQLGetInfo** ，判斷是否支援交易、是否可以將 ddl 包含在交易中，以及在交易中包含 ddl 的任何特殊效果。 如需詳細資訊，請參閱 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 函數描述。  
  
 如果驅動程式不支援交易，但應用程式 (能夠使用 ODBC) 以外的 API 來鎖定和解除鎖定資料，則應用程式可以視需要鎖定和解除鎖定記錄和資料表，以達成交易支援。 若要執行帳戶轉移範例，應用程式會鎖定這兩個帳戶的記錄、複製目前的值、為第一個帳戶付款、以第二個帳戶為點數，並解除鎖定記錄。 如果任何步驟失敗，應用程式會使用這些複本來重設帳戶。  
  
 即使是支援交易的資料來源，也可能無法在特定環境中支援多個交易。 應用程式會使用 SQL_MULTIPLE_ACTIVE_TXN 選項來呼叫 **SQLGetInfo** ，以判斷資料來源是否可以在相同環境中支援多個連接的同時使用中交易。 因為每個連線都有一個交易，所以只有具有相同資料來源之多個連接的應用程式才會感興趣。
