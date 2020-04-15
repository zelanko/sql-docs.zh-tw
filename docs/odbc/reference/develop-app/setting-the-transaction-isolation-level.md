---
title: 設定交易隔離等級 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- isolation levels [ODBC]
- transaction isolation [ODBC]
- transactions [ODBC], isolation
ms.assetid: 64a037f0-5065-4f45-9669-6710404a540c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 80401b276355a47469355cb6921d768d168398ae
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299808"
---
# <a name="setting-the-transaction-isolation-level"></a>設定交易隔離等級
要設置事務隔離級別,應用程式使用SQL_ATTR_TXN_ISOLATION連接屬性。 如果數據源不支援請求的隔離級別,驅動程式或數據源可以設置更高的級別。 要確定資料來源支援哪些事務隔離等級以及預設隔離等級是什麼,應用程式分別使用SQL_TXN_ISOLATION_OPTION和SQL_DEFAULT_TXN_ISOLATION選項調用**SQLGetInfo。**  
  
 較高的事務隔離級別為資料庫數據的完整性提供了最大的保護。 可序列化事務保證不受其他事務的影響,因此保證保持資料庫完整性。  
  
 但是,較高的事務隔離級別可能會導致性能降低,因為它會增加應用程序必須等待數據釋放鎖的可能性。 在以下情況下,應用程式可以指定較低的隔離等級以提高性能:  
  
-   當可以保證不存在可能干擾應用程式事務的其他事務時。 這種情況僅在有限的情況下發生,例如,當一個小公司中的一個人維護 dBASE 檔,這些檔在一台電腦上包含人員數據,並且不共用這些檔時。  
  
-   當速度比精度更重要,並且任何錯誤都可能很小時。 例如,假設一家公司銷售很少,而且銷售量大是罕見的。 估計所有未結銷售總價值的事務可能安全地使用未提交的讀取隔離級別。 儘管事務將包括正在打開或關閉並隨後回滾的訂單,但通常這些訂單會相互取消,並且事務會更快,因為它不會每次遇到此類訂單時被阻止。  
  
 有關詳細資訊,請參閱[樂觀併發](../../../odbc/reference/develop-app/optimistic-concurrency.md)。
