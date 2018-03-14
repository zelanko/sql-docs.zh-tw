---
title: "SQL Server 複寫 | Microsoft Docs"
ms.custom: 
ms.date: 03/30/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- replication [SQL Server], about
- replication [SQL Server]
ms.assetid: 3a5f4592-3c61-4b4d-9ceb-39716aeeba41
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Active
ms.openlocfilehash: a8694481974c19fdc9d035ab0c2185fe640e14f1
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/08/2018
---
# <a name="sql-server-replication"></a>SQL Server 複寫
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  複寫是指，將資料和資料庫物件從某個資料庫複製和散發到另一個資料庫，然後在兩個資料庫之間進行同步處理，以維護一致性的一組技術。 使用複寫，以透過區域網路、廣域網路、撥號連接、無線連接及網際網路，將資料散發到不同的位置，以及散發到遠端或行動使用者。  
  
 異動複寫一般用於需要高輸送量的伺服器對伺服器案例中，其中包括：提升延展性和可用性、資料倉儲和報表、整合多個站台的資料、整合異質資料，以及卸載批次處理。 合併式複寫主要是為了可能具有資料衝突的行動應用程式或分散式伺服器應用程式而設計。 常見的案例包括：與行動使用者交換資料、消費者銷售點 (POS) 應用程式，以及多個站台的資料整合。 快照式複寫用於提供交易式和合併式複寫的初始資料集；它也可以用於適合將資料完全重新整理時。 使用這三種複寫， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供了強大且彈性的系統，可同步處理您企業中的資料。 [!INCLUDE[win8srv](../../includes/win8srv-md.md)] 和 [!INCLUDE[win8](../../includes/win8-md.md)]支援複寫至 SQLCE 3.5 和 SQLCE 4.0。  
  
 複寫的替代方法是使用 Microsoft Sync Framework 以同步處理資料庫。 Sync Framework 包含多個元件以及一個直覺式且彈性的 API，而此 API 可簡化 SQL Server、SQL Server Express、SQL Server Compact 和 SQL Azure 資料庫之間的同步處理。 Sync Framework 也會包含類別，您可以調整這些類別以同步處理 SQL Server 資料庫與 ADO.NET 相容的任何其他資料庫。 如需 Sync Framework 資料庫同步處理元件的詳細文件，請參閱 [同步處理資料庫](http://go.microsoft.com/fwlink/?LinkId=209079)。 如需 Sync Framework 的概觀，請參閱 [Microsoft Sync Framework 開發人員中心](http://go.microsoft.com/fwlink/?LinkId=209078)。 如需 Sync Framework 與合併式複寫的比較，請參閱 [概觀和案例](http://msdn.microsoft.com/library/bb902818\(SQL.110\).aspx)。  
  
 **依區域瀏覽**  
 - [新功能](../../relational-databases/replication/what-s-new-replication.md)  
 - [回溯相容性](../../relational-databases/replication/replication-backward-compatibility.md)  
 - [複寫功能及工作](../../relational-databases/replication/replication-features-and-tasks.md)  
 - [技術參考](../../relational-databases/replication/technical-reference-replication.md)  
  
  
