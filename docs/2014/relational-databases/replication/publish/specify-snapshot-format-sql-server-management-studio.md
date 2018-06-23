---
title: 指定快照集格式 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- snapshots [SQL Server replication], formats
- snapshot replication [SQL Server], formats
ms.assetid: 7c95f545-731a-4743-9acb-0b325ef9b98b
caps.latest.revision: 36
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 0f3d7042d4359b31764fdeefbe4f42a281ed1849
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031837"
---
# <a name="specify-snapshot-format-sql-server-management-studio"></a>指定快照集格式 (SQL Server Management Studio)
  在 [發行集屬性 - \<發行集>] 對話方塊的 [快照集] 頁面上，指定快照集格式。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Publication Properties](view-and-modify-publication-properties.md)＞。  
  
### <a name="to-specify-snapshot-format"></a>若要指定快照集格式  
  
1.  在 [發行集屬性 - \<發行集>] 對話方塊的 [快照集] 頁面上，選取 [原生 SQL Server - 所有訂閱者都必須是執行 SQL Server 的伺服器] 或 [字元 - 如果發行者或訂閱者沒有執行 SQL Server 則需要]。  
  
    > [!NOTE]  
    >  建議選取原生格式，除非此發行集必須支援對 [!INCLUDE[ssEW](../../../includes/ssew-md.md)] 資料庫或非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫的訂閱。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [設定快照集屬性 &#40;複寫 Transact-SQL 程式設計&#41;](configure-snapshot-properties-replication-transact-sql-programming.md)   
 [變更發行集與發行項屬性](change-publication-and-article-properties.md)   
 [使用快照集初始化訂閱](../initialize-a-subscription-with-a-snapshot.md)  
  
  