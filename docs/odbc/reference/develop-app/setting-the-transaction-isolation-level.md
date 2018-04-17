---
title: 設定交易隔離層級 |Microsoft 文件
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
ms.topic: article
helpviewer_keywords:
- isolation levels [ODBC]
- transaction isolation [ODBC]
- transactions [ODBC], isolation
ms.assetid: 64a037f0-5065-4f45-9669-6710404a540c
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 96fff370bcde4b6cc63c7b9af97c3eced3061d85
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="setting-the-transaction-isolation-level"></a>設定交易隔離層級
若要設定交易隔離等級，應用程式會使用 SQL_ATTR_TXN_ISOLATION 連接屬性。 如果資料來源不支援要求的隔離等級，驅動程式或資料來源就可以設定較高的層級。 若要判斷何種交易隔離層級的資料來源支援並預設隔離等級時，應用程式呼叫**SQLGetInfo**與 SQL_TXN_ISOLATION_OPTION 和 SQL_DEFAULT_TXN_ISOLATION 選項，分別。  
  
 較高的交易隔離等級會提供資料庫資料的完整性大部分的防護。 可序列化的交易是保證不會受到其他交易，因此保證維護資料庫的完整性。  
  
 不過，較高的交易隔離等級可能會降低效能，因為它會增加應用程式必須等待鎖定釋出資料的可能性。 應用程式可以指定較低層級的隔離，以提升效能，在下列情況：  
  
-   當它可以保證沒有其他交易存在，可能會影響應用程式的交易。 這種情況只會發生在少數情況下，例如小型公司中的一個人時維護 dBASE 檔案，其中包含一部電腦上的個人資料，並不會共用這些檔案。  
  
-   如果速度是更為重要精確度及任何錯誤，可能會變小。 例如，假設公司可讓許多小型銷售和大型的業績很少。 估計的所有開啟的銷售量的總計值的交易可能會安全地使用 Read Uncommitted 隔離等級。 雖然交易會包含訂單，開啟或關閉而且後續會回復，這些會通常相互抵銷，而且交易會更快，因為每次它發現這類訂單，並不會封鎖它。  
  
 如需詳細資訊，請參閱[開放式並行存取](../../../odbc/reference/develop-app/optimistic-concurrency.md)。
