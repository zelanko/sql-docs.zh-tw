---
title: 教學課程：利用行動用戶端複寫資料 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: af673514-30c7-403a-9d18-d01e1a095115
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c36eae0ca3d9613dfdaf13bce3a5e748f91b123f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63255402"
---
# <a name="tutorial-replicating-data-with-mobile-clients"></a>教學課程：利用行動用戶端複寫資料
  對於在中央伺服器與只是偶爾連接的行動用戶端之間移動資料的問題，複寫是一個很好的解決方案。 您可以使用複寫的精靈，輕鬆設定及管理複寫拓撲。 本教學課程告訴您，如何為行動用戶端設定複寫拓撲。  
  
## <a name="what-you-will-learn"></a>學習內容  
 在本教學課程中，您將使用合併複寫，從中央資料庫發行資料給一個或多個行動用戶端使用者，讓每一個使用者都取得獨一無二篩選的資料子集。 第 1 課告訴您如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 建立發行集。 接下來的課程會告訴您，如何建立及同步處理訂閱。  
  
## <a name="requirements"></a>需求  
 此教學課程是特別提供給熟悉基本資料庫作業但對複寫經驗有限的使用者。 開始進行本教學課程之前，您必須先完成[教學課程：準備伺服器進行](tutorial-preparing-the-server-for-replication.md)複寫。  
  
 若要使用這個教學課程，系統上必須已安裝下列元件：  
  
-   在發行者伺服器 (來源)：  
  
    -   任何版本的 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，除了 Express ([!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]) 或 [!INCLUDE[ssEW](../../includes/ssew-md.md)]以外。 這兩種版本無法做為複寫發行者。  
  
    -   [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 範例資料庫。 為了加強安全性，依預設，不會安裝範例資料庫。  
  
-   訂閱者伺服器 (目的地)：  
  
    -   任何版本的 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，除了 [!INCLUDE[ssEW](../../includes/ssew-md.md)]以外。 
  [!INCLUDE[ssEW](../../includes/ssew-md.md)] 不受本教學課程建立的發行集支援。  
  
    > [!NOTE]  
    >  依預設，複寫未安裝在 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]中。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，您必須使用 sysadmin 固定伺服器角色成員的登入，連接到發行者和訂閱者。  
  
 **完成本教學課程的估計時間：30分鐘。**  
  
## <a name="lessons-in-this-tutorial"></a>本教學課程中的課程  
  
-   [第1課：使用合併式複寫發行資料](lesson-1-publishing-data-using-merge-replication.md)  
  
-   [第2課：建立合併式發行集的訂閱](lesson-2-creating-a-subscription-to-the-merge-publication.md)  
  
 [開始教學課程](merge/merge-replication.md)  
  
## <a name="see-also"></a>另請參閱  
 [複寫程式設計概念](concepts/replication-programming-concepts.md)  
  
  
