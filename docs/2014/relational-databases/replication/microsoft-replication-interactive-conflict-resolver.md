---
title: Microsoft 複寫互動式衝突解析程式 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.replconflictviewer.interactiveresolver.f1
ms.assetid: d3d4a480-782b-4b1d-b839-565c8cf6cb24
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6c1637301eb6a6c9663f122e61447b9a8adb1623
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48213581"
---
# <a name="microsoft-replication-interactive-conflict-resolver"></a>Microsoft Replication Interactive Conflict Resolver
  Interactive Conflict Resolver 可用於使用 Windows Synchronization Manager 同步處理的合併訂閱。 它可以讓您針對資料衝突，進行檢視、比較、編輯以及選取結果。 複寫還包含衝突檢視器，它可以讓您在認可衝突結果之後，還能夠進行檢視及修改。 Interactive Conflict Resolver 可以讓您在同步處理期間選取結果。  
  
> [!NOTE]  
>  「互動解析程式」中不會顯示涉及邏輯記錄的衝突。 若要檢視這些衝突的相關資訊，請使用複寫預存程序。 如需詳細資訊，請參閱[檢視合併式發行集的衝突資訊 &#40;複寫 Transact-SQL 程式設計&#41;](view-conflict-information-for-merge-publications.md)。  
  
## <a name="options"></a>選項。  
 **資料行名稱**  
 資料表中所有資料行的名稱。 一或多個資料行可能有衝突的資料。 無論是哪些資料行發生衝突，整個成功的資料列會覆寫整個失敗的資料列。  
  
 **建議的解決方案**  
 Conflict Resolver 針對發行項所提供的建議解決方案。  
  
 **發行者**  
 在發行者端的資料值。  
  
 **訂閱者**  
 在訂閱者端的資料值。  
  
 **接受建議**、 **接受發行者**，以及 **接受訂閱者**  
 按一下即可接受會套用在發行者端或訂閱者端的資料列 (視何者於衝突中失敗而定)。 如果發行者在衝突中失敗了，其他所有訂閱者在下次與發行者同步處理時，就會接收到成功的資料列。  
  
 **自動解決其餘衝突**  
 使用 Conflict Resolver 針對發行項所提供的建議解決方案，來解決其餘所有的衝突。  
  
 **記錄衝突的詳細資料以供日後參考。**  
 記錄系統資料表中衝突的詳細資料。  
  
## <a name="see-also"></a>另請參閱  
 [互動式衝突解決方法](merge/advanced-merge-replication-conflict-interactive-resolution.md)   
 [檢視並解決合併式發行集的資料衝突 &#40;SQL Server Management Studio&#41;](view-and-resolve-data-conflicts-for-merge-publications.md)   
 [使用 Windows Synchronization Manager 同步處理訂閱 &#40;Windows Synchronization Manager&#41;](synchronize-a-subscription-using-windows-synchronization-manager.md)   
 [Advanced Merge Replication Conflict Detection and Resolution](merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  
