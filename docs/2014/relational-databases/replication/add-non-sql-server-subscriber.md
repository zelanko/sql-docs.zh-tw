---
title: 新增非 SQL Server 訂閱者 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.rep.newsubwizard.addnonsqlsubscriber.f1
ms.assetid: 21beeaa0-4b9e-48da-be63-1b9ff14e03d2
caps.latest.revision: 10
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 53575d47aa541ec59a3c9e3003795c5321f6f0d3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37157949"
---
# <a name="add-non-sql-server-subscriber"></a>加入非 SQL Server 訂閱者
  複寫可以支援為 Oracle 和 IBM DB2 訂閱者建立快照式和交易式發行集的發送訂閱。  
  
## <a name="options"></a>選項。  
 **要加入的訂閱者類型**  
 選取 Oracle 訂閱者或 IBM DB2 訂閱者。 如需這些訂閱者支援的詳細資訊，請參閱[非 SQL Server 訂閱者](non-sql/non-sql-server-subscribers.md)。  
  
 **資料來源名稱**  
 在用來尋找網路上之資料庫的名稱。 複寫會使用資料來源名稱，結合登入、密碼及您在此精靈的 **[散發代理程式安全性]** 頁面中指定的任何連接選項，來產生資料庫的連接字串。  
  
> [!NOTE]  
>  The data source name and connection string are not validated by [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] until the Distribution Agent attempts to initialize the subscription.  
  
## <a name="see-also"></a>另請參閱  
 [為非 SQL Server 訂閱者建立訂閱](create-a-subscription-for-a-non-sql-server-subscriber.md)   
 [Non-SQL Server Subscribers](non-sql/non-sql-server-subscribers.md)   
 [訂閱發行集](subscribe-to-publications.md)  
  
  
