---
title: "互動式衝突解決方法 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interactive conflict resolution [SQL Server replication]
- interactive resolver [SQL Server replication]
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 172c60c7-f605-4eb5-b185-54ae9e9d3c60
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 410b9b720455a699ced2b276df7e76d442cf380e
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="advanced-merge-replication-conflict---interactive-resolution"></a>進階合併式複寫衝突 - 互動式解決方法
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] replication provides an Interactive Resolver, which allows you to resolve conflicts manually during on-demand synchronization in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows Synchronization Manager. 「互動解析程式」是圖形介面，會在執行時期啟動並顯示各衝突資料列的資料，以及提供檢視及編輯衝突資料的選項，然後個別解決每項衝突。  
  
 「互動解析程式」與「衝突檢視器」相類似。 「衝突檢視器」是顯示合併同步之後已解決的衝突結果，而「互動解析程式」則顯示解決之前的每個衝突，並在合併同步期間讓您決定每個衝突的結果。 在衝突發生時應有人監視「互動解析程式」。  
  
> [!NOTE]  
>  「互動式解決」需要 Windows Synchronization Manager。 如果是在 Windows Synchronization Manager 之外執行同步處理 (如 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 或複寫監視器中已排程的同步處理或視需要同步處理)，則不需要使用者的介入，就會根據為發行項指定的解決器自動解決衝突。 「互動解析程式」中不會顯示涉及邏輯記錄的衝突。 若要檢視這些衝突的相關資訊，請使用複寫預存程序。 如需詳細資訊，請參閱[檢視合併式發行集的衝突資訊 &#40;複寫 Transact-SQL 程式設計&#41;](../../../relational-databases/replication/view-conflict-information-for-merge-publications.md)。  
  
## <a name="article-resolvers-and-the-interactive-resolver"></a>發行項解析程式與互動解析程式  
 衝突解析程式 (預設解析程式、商務邏輯處理常式或自訂解析程式) 會在發行集建立時指派給特定的發行項，並利用一組規則來決定衝突資料列資料輸入時應使用那一組資料。 「互動解析程式」並不是一個具有可決定衝突中成功者與失敗者的獨立衝突解析程式，它只是一個搭配預設與自訂解析程式使用的工具。 發行項解析程式仍會決定成功與失敗的資料列，但「互動解析程式」可讓使用者介入以接受、拒絕或修改結果。  
  
 若要使用「互動解析程式」，必須為每個發行項以及需要它的訂閱啟用互動式解決。 為一個或多個發行項和訂閱啟用「互動解析程式」之後，便會在合併同步處理期間偵測到衝突時使用它。  
  
 若要使用互動解析程式，請參閱[指定合併發行項的互動式衝突解決方法](../../../relational-databases/replication/publish/specify-interactive-conflict-resolution-for-merge-articles.md)和[使用 Windows Synchronization Manager 同步處理訂閱 &#40;Windows Synchronization Manager&#41;](../../../relational-databases/replication/synchronize-a-subscription-using-windows-synchronization-manager.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Advanced Merge Replication Conflict Detection and Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  
