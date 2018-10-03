---
title: 自動認可模式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- rolling back transactions [ODBC]
- auto-commit mode [ODBC]
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
- transactions [ODBC], rolling back
ms.assetid: c8de5b60-d147-492d-b601-2eeae8511d00
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 87a5bababd2129ffb7e0aad36a2ceb3362d4acd9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47792356"
---
# <a name="auto-commit-mode"></a>自動認可模式
*在自動認可模式下，* 每個資料庫作業若未執行時未認可的交易。 此模式非常適合許多組成單一的 SQL 陳述式的實際交易。 它不需要分隔或指定這些交易完成。 在資料庫中沒有交易支援，自動認可模式是唯一支援的模式。 在這類資料庫中，陳述式會認可時就會執行並沒有任何方法來回復它們;他們因此一律是自動認可模式。  
  
 如果基礎 DBMS 不支援自動認可模式的交易，此驅動程式可以模擬它們執行時，以手動方式認可每個 SQL 陳述式。  
  
 如果在自動認可模式下執行的 SQL 陳述式批次時，它是資料來源特定批次中的陳述式的認可。 它們可以認可執行，或整個批次執行完成之後。 某些資料來源可能支援以上兩種行為，並且可能會提供一種選取下列其中之一或其他人。 特別的是，如果批次的中間，發生錯誤，則資料來源專用是否已經執行的陳述式來認可或回復。 因此，互通的應用程式，使用批次，並要求他們應該認可或回復整個應該只能在手動認可模式中執行批次。
