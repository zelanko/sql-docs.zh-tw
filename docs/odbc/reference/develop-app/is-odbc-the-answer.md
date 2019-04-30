---
title: 答案是 ODBC 嗎？ | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], ODBC
ms.assetid: bfa5e6ee-5979-42a9-be6f-a84d1ee7a54c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f90f2395eac5dce76848d7bc309f1a3d5ce289f9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63179899"
---
# <a name="is-odbc-the-answer"></a>答案是 ODBC 嗎？
在探究之前的互通性問題，請考慮下列問題：應用程式應該使用 ODBC 完全嗎？ 這看起來似乎很奇怪的問題 ODBC，指南中，但它其實只是，合法。 ODBC 的設計無法完全取代原生資料庫 Api，也就設計來提供在所有情況下的資料庫存取權。 它設計來提供資料庫的通用介面，要用來釋放應用程式設計人員不必了解和維護多個資料庫的連結。  
  
 自訂的應用程式是原生資料庫 Api 的最佳候選項。 自訂應用程式通常使用單一的 DBMS，而不需要是互通的主要原因。 原生資料庫 Api 可能會表現最好，能比 ODBC 公開特定 DBMS 的功能，並可能會公開不 ODBC 所公開的功能。 此外，自訂應用程式的開發人員熟悉通常他們 DBMS 的原生資料庫 API，因為不太需要了解 ODBC。 不過，值得注意的某些 Dbms，ODBC API 的原生資料庫。  
  
 因此哪些應用程式是適用於 ODBC 的候選項目？ 最佳候選項目是使用一個以上的 DBMS 的應用程式。 這包括幾乎所有的泛型和垂直應用程式。 它也包含一些自訂的應用程式。 例如，使用數個不同的 Dbms 的自訂應用程式會更容易、 更容易撰寫具有比使用多個原生 Api 的 ODBC。 並使用 ODBC 所撰寫的自訂應用程式會更容易移轉為公司將從不同的 DBMS 移至另一個，或將相同的應用程式，針對不同的 Dbms 部署。
