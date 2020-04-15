---
title: 提交和回滾事務 |微軟文件
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
ms.openlocfilehash: 1c272d60242d31622452c4dcb0f6a16c4838768f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299108"
---
# <a name="committing-and-rolling-back-transactions"></a>認可及回復交易
要在手動提交模式下提交或回捲此事務,應用程式將呼叫**SQLEndTran**。 支援事務的 DBMS 的驅動程式通常透過執行**COMMIT**或**ROLLBACK**語句來實現此函數。 當連接處於自動提交模式時,驅動程式管理員不調用 SQLEndTran;但是,驅動程式管理器不會調用**SQLEndTran。** 它只是返回SQL_SUCCESS,即使應用程序嘗試回滾事務。 由於不支援事務的 DBMS 的驅動程式始終處於自動提交模式,因此它們可以實現**SQLEndTran**返回SQL_SUCCESS而不執行任何操作或根本不實現它。  
  
> [!NOTE]  
>  應用程式不應透過使用 SQLExecute 或**SQLExecDirect**執行**SQLExecDirect****COMMIT**或**ROLLBACK**語句來提交或回滾事務。 執行此操作的效果未定義。 可能的問題包括驅動程式不再知道事務何時處於活動狀態,以及這些語句對不支援事務的數據源失敗。 這些應用程式應調用**SQLEndTran。**  
  
 如果應用程式將環境句柄傳遞給**SQLEndTran,** 但不傳遞連接句柄,則驅動程式管理器在概念上調用**SQLEndTran,** 並針對環境中具有一個或多個活動連接的每個驅動程式調用環境句柄。 然後,驅動程式在環境中的每個連接上提交事務。 但是,請務必認識到,驅動程式和驅動程式管理員都不會對環境中的連接執行兩階段提交;因此,駕駛員經理對環境中的連接執行兩階段提交。這隻是同時調用**SQLEndTran**環境中所有連接的程式設計便利。  
  
 (*兩階段提交*通常用於提交分佈在多個數據源的事務。 在第一階段,將輪詢數據源,以決定是否可以提交其部分事務。 在第二階段,事務實際上是在所有數據源上提交的。 如果第一階段的任何數據源答覆它們無法提交事務,則第二階段不會發生。
