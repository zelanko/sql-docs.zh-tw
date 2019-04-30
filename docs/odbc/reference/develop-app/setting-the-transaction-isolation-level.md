---
title: 設定交易隔離層級 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 37b575f9e208b5a1b7fa03b170b74633da149c67
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63237871"
---
# <a name="setting-the-transaction-isolation-level"></a>設定交易隔離等級
若要設定交易隔離等級，應用程式會使用 SQL_ATTR_TXN_ISOLATION 連接屬性。 如果資料來源不支援要求的隔離等級，驅動程式或資料來源可以設定較高的層級。 若要判斷何種交易隔離等級的資料來源支援和哪些預設隔離等級為，則應用程式會呼叫**SQLGetInfo** SQL_TXN_ISOLATION_OPTION 和 SQL_DEFAULT_TXN_ISOLATION 選項分別。  
  
 更高層級的交易隔離提供資料庫資料的完整性大部分的保護。 可序列化的交易是保證不會受到其他交易，並因此保證維護資料庫的完整性。  
  
 不過，較高層級的交易隔離可能會導致效能變慢，因為這樣會增加應用程式必須等待鎖定釋出資料的機會。 應用程式可以指定較低的層級的隔離，以提升效能，在下列情況：  
  
-   當它可以保證沒有其他交易存在，可能會干擾應用程式的交易。 這種情況下只會發生在少數情況下，例如當小型公司中的一個人會維護 dBASE 檔案，其中包含一部電腦上的個人資料，並不會共用這些檔案。  
  
-   如果速度是高於精確度和任何錯誤都可能會變小。 例如，假設某公司可讓許多小型的銷售和銷售很少。 估計的所有開啟的銷售總計值的交易可能會安全地使用 Read Uncommitted 隔離等級。 雖然交易會包含訂單正在開啟或關閉而且之後回復，這些會通常相互抵銷和交易可能快多了，因為它不會封鎖每次它遇到這類訂單。  
  
 如需詳細資訊，請參閱 <<c0> [ 開放式並行存取](../../../odbc/reference/develop-app/optimistic-concurrency.md)。
