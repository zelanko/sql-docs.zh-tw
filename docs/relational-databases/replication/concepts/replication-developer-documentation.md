---
title: "複寫開發人員文件 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- developer's guide [SQL Server replication]
- programming [SQL Server replication]
- replication [SQL Server], development
ms.assetid: 7ee134ae-1cab-4a35-8017-8ac6d8fc64b6
caps.latest.revision: "40"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b6d8c0a3227bdb30bb446b5eceeaf02354c6c29b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="replication-developer-documentation"></a>複寫開發人員文件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  以程式設計的方式設定、維護和監視複寫拓撲的能力，可讓您同時簡化重複的複寫工作，並改善複寫為主的應用程式之使用者經驗。 透過設計複寫的程式，一般使用者即可使用自訂的複寫功能，而不須熟悉複寫預存程序和複寫代理程式可執行檔，或是不須使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 實作的複寫使用者介面。  
  
 以下是您的應用程式可能從用程式存取複寫服務獲益的狀況：  
  
-   將複寫功能加入現有一般使用者應用程式，例如在使用者按一下按鈕時，同步處埋提取訂閱。  
  
-   建立供遠端管理複寫使用的網路架構使用者介面。  
  
-   建立只公開管理功能子集的自訂使用者介面，可用以從單一位置遠端管理多個複寫拓撲，或是可結合管理與同步處理功能。  
  
-   透過加入監視發行集、訂閱或是在散發者端的狀態之能力，來改善現有的監視工具。  
  
-   建立自訂應用程式以管理訂閱，或是將它們同步處理至 Oracle 發行者。  
  
-   當同步處理合併式訂閱時，會寫入執行的自訂商務邏輯規則。  
  
-   在設定新的訂閱者時，會產生可重複執行的 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 指令碼。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可讓您以程式設計的方式控制複寫代理程式，並以程式設計的方式管理和監視複寫拓撲。 若要深入了解程式設計複寫，請參閱[複寫程式設計概念](../../../relational-databases/replication/concepts/replication-programming-concepts.md)。  
  
## <a name="in-this-section"></a>本節內容  
 [複寫程式設計概念](../../../relational-databases/replication/concepts/replication-programming-concepts.md)  
 描述開發使用複寫之應用程式的規劃步驟。  
  
 [複寫系統預存程序概念](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
 描述如何使用系統預存程序，在應用程式拓撲中提供程式存取。  
  
 [複寫管理物件概念](../../../relational-databases/replication/concepts/replication-management-objects-concepts.md)  
 說明使用 Replication Management Objects (RMO) 的概念。 這是一種 Managed 程式碼組件，用以封裝 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的複寫功能。  
  
 [複寫代理程式可執行檔概念](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
 描述複寫代理程式可執行檔的使用。  
  
 [開發人員指南：使用說明主題 &#40;複寫&#41;](../../../relational-databases/replication/concepts/developer-s-guide-how-to-topics-replication.md)  
 提供與複寫相關的如何主題清單。  
  
  
