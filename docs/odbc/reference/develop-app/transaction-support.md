---
title: 交易支援 |微軟文件
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
ms.openlocfilehash: a5b9d731d12329a4ef663b1ea66cdc59a0b153fa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297976"
---
# <a name="transaction-support"></a>交易支援
對事務的支援程度是驅動程式定義的。 ODBC 設計為在單使用者或桌面資料庫上實現,無需管理其數據的多個更新。 此外,某些支援事務的資料庫僅針對 SQL 的數據操作語言 (DML) 語句執行此操作;當事務處於活動狀態時,有關數據定義語言 (DDL) 的使用存在限制或特殊事務語義。 也就是說,對於表的多個同時更新,可能存在事務支援,但對於在事務期間更改表的數量和定義,則不支援事務支援。  
  
 應用程式透過使用 SQL_TXN_CAPABLE 選項呼叫**SQLGetInfo,** 確定是否支援事務、是否可以將 DDL 包含在事務中以及將 DDL 包含在事務中的任何特殊效果。 有關詳細資訊,請參閱[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函數說明。  
  
 如果驅動程式不支援事務,但應用程式能夠(使用 ODBC 以外的 API)鎖定和解鎖數據,則應用程式可以通過根據需要鎖定和解鎖記錄和表來實現事務支援。 要實現帳戶轉移示例,應用程式將鎖定兩個帳戶的記錄、複製當前值、轉帳第一個帳戶、貸記第二個帳戶以及解鎖記錄。 如果任何步驟失敗,應用程式將使用副本重置帳戶。  
  
 即使支援事務的數據源也可能無法在特定環境中一次支援多個事務。 應用程式使用SQL_MULTIPLE_ACTIVE_TXN選項呼叫**SQLGetInfo,** 以確定資料來源是否可以支援同一環境中多個連接上同時處於活動狀態事務。 由於每個連接都有一個事務,因此對於與同一數據源具有多個連接的應用程式僅感興趣。
