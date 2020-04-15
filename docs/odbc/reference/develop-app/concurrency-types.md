---
title: 併發類型 |微軟文件
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
- locking concurrency control [ODBC]
- optimistic concurrency [ODBC]
- read-only concurrency control [ODBC]
ms.assetid: 46762ae5-17dd-4777-968e-58156f470fe1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 642301d09c5aa189276db534e58aca0c5e00e3ce
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299098"
---
# <a name="concurrency-types"></a>並行類型
為了解決游標中併發性降低的問題,ODBC 公開了四種不同類型的游標併發:  
  
-   **唯讀**游標可以讀取數據,但不能更新或刪除數據。 這是默認併發類型。 儘管 DBMS 可能會鎖定行以強制實施可重複讀取和可序列化隔離級別,但它可以使用讀取鎖而不是寫入鎖。 這將導致更高的併發性,因為其他事務至少可以讀取數據。  
  
-   **鎖定**游標使用所需的最低鎖定級別,以確保它可以更新或刪除結果集中的行。 這通常會導致非常低的併發級別,尤其是在可重複讀取和可序列化事務隔離級別。  
  
-   **使用行版本進行樂觀併發,並使用值進行樂觀併發**游標使用樂觀併發:它僅在行自上次讀取以來未更改時更新或刪除行。 為了檢測更改,它會比較行版本或值。 不能保證游標能夠更新或刪除行,但併發性遠遠高於使用鎖定時。 有關詳細資訊,請參閱以下部分"[樂觀併發](../../../odbc/reference/develop-app/optimistic-concurrency.md)"。  
  
 應用程式指定希望游標與SQL_ATTR_CONCURRENCY語句屬性一起使用的併發類型。 要確定支援哪些類型,它使用SQL_SCROLL_CONCURRENCY選項調用**SQLGetInfo。**
