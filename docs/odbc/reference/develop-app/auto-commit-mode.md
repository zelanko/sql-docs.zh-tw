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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6f19053eec7a48eba7a51425b01744f3acd10015
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81285108"
---
# <a name="auto-commit-mode"></a>自動認可模式
*在自動認可模式中，* 每個資料庫作業都是執行時認可的交易。 這種模式適用于包含單一 SQL 語句的許多真實世界交易。 不需要分隔或指定完成這些交易。 在沒有交易支援的資料庫中，自動認可模式是唯一支援的模式。 在這類資料庫中，語句會在執行時認可，而且沒有任何方法可以復原它們。因此，它們一律會處於自動認可模式。  
  
 如果基礎 DBMS 不支援自動認可模式交易，則驅動程式可以在執行每個 SQL 語句時，以手動方式加以模擬。  
  
 如果 SQL 語句的批次是在自動認可模式中執行，則在認可批次中的語句時，它會是特定的資料來源。 在執行整個批次之後，可以將它們認可，或做為整體執行。 某些資料來源可能會支援這兩種行為，而且可能會提供一種方式來選取其中一個。 特別是，如果批次中間發生錯誤，則不論已認可或回復已執行的語句，它都是資料來源特有的。 因此，使用批次的互通應用程式，需要將它們認可或回復為整體，只應在手動認可模式下執行批次。
