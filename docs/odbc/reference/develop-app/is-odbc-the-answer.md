---
title: "答案是 ODBC？ | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interoperability [ODBC], ODBC
ms.assetid: bfa5e6ee-5979-42a9-be6f-a84d1ee7a54c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2ada446a96ecb6fd81d05380c8a29707eb41f8ee
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="is-odbc-the-answer"></a>答案是 ODBC？
在深入之前的互通性問題，請考慮下列問題： 應用程式應該使用 ODBC 完全嗎？ 這似乎很奇怪 ODBC，指南中詢問問題，但很，事實上，合法。 ODBC 的設計無法完全取代原生資料庫應用程式開發介面，也就設計來提供在所有情況下的資料庫存取權。 它設計來提供資料庫的通用介面，其目的是要釋放應用程式設計人員必須了解和維護多個資料庫的連結。  
  
 自訂應用程式是以原生資料庫 Api 的主要候選。 主要原因是自訂應用程式通常使用單一的 DBMS，而且不需要互通。 原生資料庫 Api 可能會比 ODBC 公開的特定 DBMS 功能的更好，並可能會公開不 ODBC 所公開的功能。 此外，自訂應用程式的開發人員熟悉通常其 DBMS 的原生資料庫應用程式開發介面，因為沒有什麼道理，若要了解 ODBC。 不過，值得請注意，對於某些 Dbms，ODBC API 的原生資料庫。  
  
 因此哪些應用程式是 ODBC 的候選項目？ 最佳的候選方式為使用一個以上的 DBMS 應用程式。 這包括幾乎所有的一般和垂直應用程式。 它也包含一些自訂的應用程式。 例如，使用數個不同的 Dbms 自訂應用程式會更為輕鬆而且清潔撰寫使用多個原生應用程式開發介面比 ODBC。 並使用 ODBC 撰寫的自訂應用程式都能更輕鬆地從一個 DBMS 移到另一個公司，或將相同的應用程式，針對不同的 Dbms 部署移轉。

