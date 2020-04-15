---
title: 樂觀同一性 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], concurrency control
- concurrency control [ODBC]
- optimistic concurrency [ODBC]
ms.assetid: 9d71e09e-bc68-4c1f-9229-ed2a7be7d324
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 30eba3ea03b4c798a74a8cb928014b582846607b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282480"
---
# <a name="optimistic-concurrency"></a>開放式並行存取
*樂觀併發*源於一種樂觀的假設,即事務之間的衝突很少發生;當另一個事務更新或刪除當前事務讀取的時間與更新或刪除數據的時間之間的一行數據時,即發生衝突。 它與*悲觀併發*性或鎖定相反,其中應用程式開發人員認為此類衝突司空見慣。  
  
 在樂觀併發中,行保持解鎖,直到更新或刪除它的時間。 此時,將重新讀取並檢查該行,以查看自上次讀取以來是否更改了該行。 如果行已更改,更新或刪除將失敗,必須重試。  
  
 要確定行是否已更改,則會對照該行的緩存版本檢查其新版本。 此檢查可以基於行版本,例如 SQL Server 中的時間戳列或行中每列的值。 許多 DBMS 不支援行版本。  
  
 樂觀併發可以由數據源或應用程序實現。 在這兩種情況下,應用程式都應使用低事務隔離級別,如"讀取已提交";在任種情況下,應用程式都應使用"已提交"這樣的低事務隔離級別。使用較高的水準否定了使用樂觀併發獲得的增加併發。  
  
 如果樂觀併發由數據源實現,則應用程式將SQL_ATTR_CONCURRENCY語句屬性設置為SQL_CONCUR_ROWVER或SQL_CONCUR_VALUES。 要更新或刪除行,它執行定位的更新或刪除語句或調用**SQLSetPos,** 就像使用悲觀併發一樣;如果更新或刪除由於衝突而失敗,驅動程式或數據源將返回 SQLSTATE 01001(Cursor 操作衝突)。  
  
 如果應用程式本身實現樂觀併發,它將SQL_ATTR_CONCURRENCY語句屬性設置到SQL_CONCUR_READ_ONLY讀取行。 如果它將比較行版本,但不知道行版本列,它將使用SQL_ROWVER選項調用**SQLSpecialColumn**以確定此列的名稱。  
  
 應用程式通過增加與SQL_CONCUR_LOCK併發(獲取對行的寫入存取許可權)以及使用**WHERE**子句執行**更新**或**DELETE**語句來更新或刪除該行,該語句指定該行讀取該行時的版本或值。 如果此後該行已更改,則語句將失敗。 如果**WHERE**子句不唯一標識該行,則語句也可能更新或刪除其他行;否則,該語句也可能更新或刪除其他行。行版本始終唯一標識行,但行值僅在包含主鍵時才唯一標識行。
