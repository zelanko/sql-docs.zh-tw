---
title: 設定交易隔離等級 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299808"
---
# <a name="setting-the-transaction-isolation-level"></a>設定交易隔離等級
若要設定交易隔離等級，應用程式會使用 SQL_ATTR_TXN_ISOLATION 連接屬性。 如果資料來源不支援要求的隔離等級，則驅動程式或資料來源可以設定較高的層級。 為了判斷資料來源支援的交易隔離等級和預設隔離等級為何，應用程式會分別使用 SQL_TXN_ISOLATION_OPTION 和 SQL_DEFAULT_TXN_ISOLATION 選項來呼叫**SQLGetInfo** 。  
  
 較高的交易隔離層級可為資料庫資料的完整性提供最大的保護。 可序列化的交易保證不會受到其他交易的影響，因此保證會維持資料庫的完整性。  
  
 不過，較高的交易隔離層級可能會導致效能變慢，因為這會增加應用程式必須等候資料鎖定的機會。 在下列情況下，應用程式可以指定較低的隔離層級來提升效能：  
  
-   當可以保證不存在任何其他交易可能會干擾應用程式的交易。 只有在有限的情況下才會發生這種情況，例如當小型公司中的一個人在一部電腦上維護包含人員資料的 dBASE 檔案，而不共用這些檔案時。  
  
-   當速度比精確度更重要，而且任何錯誤都可能很小。 例如，假設某家公司做出許多小型銷售，而大型銷售很罕見。 估計所有開放式銷售的總計值的交易，可能會安全地使用讀取未認可的隔離等級。 雖然交易會包含已開啟或已關閉的訂單，且後續會回復，但這些情況通常會取消彼此，而交易的速度會更快，因為每次遇到這類訂單時，都不會封鎖該交易。  
  
 如需詳細資訊，請參閱[開放式並行](../../../odbc/reference/develop-app/optimistic-concurrency.md)存取。
