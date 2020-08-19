---
description: 自動認可模式
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
ms.openlocfilehash: af4b532a2163f0c30a3bdb792cfada6bdf806c43
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476890"
---
# <a name="auto-commit-mode"></a>自動認可模式
*在自動認可模式中，* 每個資料庫作業都是在執行時認可的交易。 這種模式適用于許多由單一 SQL 語句組成的真實世界交易。 不需要分隔或指定完成這些交易。 在沒有交易支援的資料庫中，自動認可模式是唯一支援的模式。 在這類資料庫中，語句會在執行時進行認可，且沒有任何方法可將它們復原;因此，它們一律會處於自動認可模式。  
  
 如果基礎 DBMS 不支援自動認可模式交易，則驅動程式可以在執行時手動認可每個 SQL 語句來模擬它們。  
  
 如果在自動認可模式下執行 SQL 語句批次，當批次中的語句認可時，它就會是資料來源特有的。 您可以在執行整個批次之後，以執行或整個批次的方式進行認可。 某些資料來源可能會支援這兩種行為，而且可能會提供一種方式來選取其中一個。 尤其是，如果批次中間發生錯誤，則不論是否已認可或回復已執行的語句，它都是資料來源特有的。 因此，使用批次並要求它們以整體方式認可或復原的互通應用程式，應該只在手動認可模式中執行批次。
