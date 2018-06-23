---
title: 初始化訂閱 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- snapshot replication [SQL Server], initializing subscriptions
- transactional replication, initializing subscriptions
- initializing subscriptions [SQL Server replication]
- subscriptions [SQL Server replication], initializing
- initializing subscriptions [SQL Server replication], about initializing subscriptions
- merge replication [SQL Server replication], initializing subscriptions
ms.assetid: d6013845-cb7a-4203-8e21-edce32f1d330
caps.latest.revision: 31
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 0aa0d72f414d26650d2eefe8ef9d54682d4bbd05
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36034761"
---
# <a name="initialize-a-subscription"></a>初始化訂閱
  複寫拓撲中的訂閱者必須初始化，使得它們具有已訂閱發行集中各發行項之結構描述副本和所有需要的複寫物件，例如預存程序、觸發程序和中繼資料表。 另外，「訂閱者」通常會接收初始資料集。 預設初始化方法會使用包含結構描述、複寫物件和資料的完整快照集，但是沒有完整的快照集也可以初始化發行集。  
  
 如需相關資訊，請參閱 [Initialize a Subscription with a Snapshot](initialize-a-subscription-with-a-snapshot.md) 及 [Initialize a Transactional Subscription Without a Snapshot](initialize-a-transactional-subscription-without-a-snapshot.md)。  
  
  