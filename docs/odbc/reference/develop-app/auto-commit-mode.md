---
title: "自動認可模式 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- rolling back transactions [ODBC]
- auto-commit mode [ODBC]
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
- transactions [ODBC], rolling back
ms.assetid: c8de5b60-d147-492d-b601-2eeae8511d00
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b2a9fd1565d0980e5af77d3cded499ce1f0091e5
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="auto-commit-mode"></a>自動認可模式
*在自動認可模式下，*每個資料庫作業若未執行時未認可的交易。 此模式是適用於單一 SQL 陳述式所組成的許多實際的交易。 它不需要分隔或指定這些交易完成。 在資料庫中沒有交易支援，自動認可模式是唯一支援的模式。 在這類資料庫中，陳述式時，會認可它們執行而沒有任何方法，將其復原;它們因此一律會在自動認可模式。  
  
 如果基礎 DBMS 不支援自動認可模式的交易，驅動程式可以模擬它們執行時以手動方式認可每個 SQL 陳述式。  
  
 如果在自動認可模式下執行的 SQL 陳述式批次，則它是資料來源專用，認可批次中的陳述式時也一樣。 它們可以認可執行，或整個批次執行完成之後。 某些資料來源支援以上兩種行為，而且可能提供的其中一個或其他的方式。 特別是，如果批次的中間，發生錯誤，則資料來源專用是否已執行的陳述式來認可或回復。 因此，互通的應用程式，使用批次，並要求他們認可或回復整個應該只能在手動認可模式中執行批次。
