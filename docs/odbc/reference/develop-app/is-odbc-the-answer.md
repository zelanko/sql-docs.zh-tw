---
description: 答案是 ODBC 嗎？
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
ms.openlocfilehash: 7a51c4248a041d65f00ec1846f60788cded68f7b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476600"
---
# <a name="is-odbc-the-answer"></a>答案是 ODBC 嗎？
在探究互通性的問題之前，請先考慮下列問題：應用程式是否應該完全使用 ODBC？ 這似乎是一個奇怪的問題，可詢問 ODBC 的指南，但實際上是合法的問題。 ODBC 不是設計來完全取代原生資料庫 Api，也不是為了在所有情況下提供資料庫存取而設計的。 它是設計用來提供資料庫的通用介面，目的是要讓應用程式設計人員不必學習和維護多個資料庫的連結。  
  
 自訂應用程式是原生資料庫 Api 的主要候選項目。 主要的原因是，自訂應用程式通常會使用單一 DBMS，且不需要互通。 原生資料庫 Api 所做的作業，可能比 ODBC 公開特定 DBMS 的功能更好，而且可能會公開 ODBC 未公開的功能。 此外，因為自訂應用程式的開發人員通常很熟悉其 DBMS 的原生資料庫 API，所以學習 ODBC 的原因很少。 不過，請注意，對於某些 Dbms 而言，ODBC 是原生資料庫 API。  
  
 哪些應用程式是 ODBC 的候選項目？ 最適合使用的應用程式是使用一個以上的 DBMS。 這包括幾乎所有的泛型和垂直應用程式。 它也包含許多自訂應用程式。 例如，使用數個不同 Dbms 的自訂應用程式，與使用 ODBC 撰寫的自訂應用程式比使用多個原生 Api 更簡單、更簡潔。 而以 ODBC 撰寫的自訂應用程式，在公司從某個 DBMS 移至另一個 DBMS 或針對不同 Dbms 部署相同的應用程式時，就更容易遷移。
