---
title: "教學課程：在連續連接的伺服器之間複寫資料 | Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
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
applies_to:
- SQL Server 2016
helpviewer_keywords:
- tutorials [SQL Server replication]
- replication [SQL Server], tutorials
- wizards [SQL Server replication]
ms.assetid: 7b18a04a-2c3d-4efe-a0bc-c3f92be72fd0
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 62fa700f137037241904f927060e4a598d132928
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/08/2018
---
# <a name="tutorial-replicating-data-between-continuously-connected-servers"></a>教學課程：在連續連接的伺服器之間複寫資料
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
對於在連續連接的伺服器之間移動資料的問題，複寫是一個很好的解決方案。 您可以使用複寫的精靈，輕鬆設定及管理複寫拓撲。 本教學課程告訴您，如何為連續連接的伺服器設定複寫拓撲。  
  
## <a name="what-you-will-learn"></a>學習內容  
本教學課程告訴您如何使用異動複寫，從一個資料庫將資料發行到另一個資料庫。 第 1 課告訴您如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 建立發行集。 接下來的課程會告訴您，如何建立及驗證訂閱，以及如何測量延遲。  
  
## <a name="requirements"></a>需求  
本教學課程是特別提供給熟悉基本資料庫作業但對複寫經驗有限的使用者。 本教學課程需要您完成上一個教學課程： [準備伺服器進行複寫](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md)。  
  
若要使用這個教學課程，系統上必須已安裝下列元件：  
  
-   在發行者伺服器 (來源)：  
  
    -   任何版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，除了 Express ([!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]) 或 [!INCLUDE[ssEW](../../includes/ssew-md.md)]以外。 這兩種版本無法做為複寫發行者。  
  
    -   [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 範例資料庫。 為了加強安全性，依預設，不會安裝範例資料庫。  
  
-   訂閱者伺服器 (目的地)：  
  
    -   任何版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，除了 [!INCLUDE[ssEW](../../includes/ssew-md.md)]以外。 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 在異動複寫中不能是訂閱者。  
  
    > [!NOTE]  
    > 依預設，複寫未安裝在 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 中。  
  
> [!NOTE]  
> 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，您必須使用 **系統管理員 (sysadmin)** 固定伺服器角色成員的登入，連接到發行者和訂閱者。  
  
**完成本教學課程的估計時間：30 分鐘。**  
  
## <a name="lessons-in-this-tutorial"></a>本教學課程中的課程  
  
-   [第 1 課：使用異動複寫發行資料](../../relational-databases/replication/lesson-1-publishing-data-using-transactional-replication.md)  
  
-   [第 2 課：建立交易式發行集的訂閱](../../relational-databases/replication/lesson-2-creating-a-subscription-to-the-transactional-publication.md)  
  
-   [第 3 課：驗證訂閱及測量延遲](../../relational-databases/replication/lesson-3-validating-the-subscription-and-measuring-latency.md)  
  
[開始教學課程](../../relational-databases/replication/lesson-1-publishing-data-using-transactional-replication.md)  
  
## <a name="see-also"></a>另請參閱  
[複寫程式設計概念](../../relational-databases/replication/concepts/replication-programming-concepts.md)  
  
  
  
