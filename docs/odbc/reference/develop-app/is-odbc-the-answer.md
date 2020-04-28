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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f3716acbcc1b8ea648b5edc03e277983936da557
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81288089"
---
# <a name="is-odbc-the-answer"></a>答案是 ODBC 嗎？
在探究互通性的問題之前，請考慮下列問題：應用程式是否應該使用 ODBC？ 這似乎是一個奇怪的問題，可以詢問 ODBC 的指南，但事實上，這也是合法的。 ODBC 的設計不是要完全取代原生資料庫 Api，而是設計成在所有情況下都不提供資料庫存取。 其設計目的是要為資料庫提供通用介面，並讓應用程式設計人員不必瞭解和維護多個資料庫的連結。  
  
 自訂應用程式是原生資料庫 Api 的主要候選項目。 主要的原因是自訂應用程式通常會使用單一 DBMS，而不需要互通。 原生資料庫 Api 所做的作業，可能會比 ODBC 公開特定 DBMS 的功能更好，而且可能會公開 ODBC 未公開的功能。 此外，由於自訂應用程式的開發人員通常會熟悉其 DBMS 的原生資料庫 API，因此不太可能瞭解 ODBC。 不過，要特別注意的是，在某些 Dbms 中，ODBC 是原生資料庫 API。  
  
 那麼，哪些應用程式是 ODBC 的候選項目？ 最佳的候選項目是使用多個 DBMS 的應用程式。 這包括幾乎所有的一般和垂直應用程式。 它也包含許多自訂應用程式。 例如，使用數個不同 Dbms 的自訂應用程式，會比使用多個原生 Api 更容易且更清楚地寫入 ODBC。 使用 ODBC 撰寫的自訂應用程式更容易遷移，因為公司會從一個 DBMS 移至另一個，或針對不同的 Dbms 部署相同的應用程式。
