---
description: Microsoft Replication Interactive Conflict Resolver
title: 互動式衝突解析程式 (合併式)
describes: Describes the Interactive Conflict Resolver that can be used for merge subscriptions that are synchronized using the Windows Synchronization Manager.
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.replconflictviewer.interactiveresolver.f1
ms.assetid: d3d4a480-782b-4b1d-b839-565c8cf6cb24
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016
ms.openlocfilehash: a0cbd836bc0a7676128067f44e4079d4901de962
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97464719"
---
# <a name="microsoft-replication-interactive-conflict-resolver"></a>Microsoft Replication Interactive Conflict Resolver
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Interactive Conflict Resolver 可用於使用 Windows Synchronization Manager 同步處理的合併訂閱。 它可以讓您針對資料衝突，進行檢視、比較、編輯以及選取結果。 複寫還包含衝突檢視器，它可以讓您在認可衝突結果之後，還能夠進行檢視及修改。 Interactive Conflict Resolver 可以讓您在同步處理期間選取結果。  
  
> [!NOTE]  
>  「互動解析程式」中不會顯示涉及邏輯記錄的衝突。 若要檢視這些衝突的相關資訊，請使用複寫預存程序。 如需詳細資訊，請參閱[檢視合併式發行集的衝突資訊 &#40;複寫 Transact-SQL 程式設計&#41;](./view-and-resolve-data-conflicts-for-merge-publications.md)。  
  
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
 [互動式衝突解決方法](../../relational-databases/replication/merge/advanced-merge-replication-conflict-interactive-resolution.md)   
 [檢視並解決合併式發行集的資料衝突 &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/view-and-resolve-data-conflicts-for-merge-publications.md)   
 [使用 Windows Synchronization Manager 同步處理訂閱 &#40;Windows Synchronization Manager&#41;](../../relational-databases/replication/synchronize-a-subscription-using-windows-synchronization-manager.md)   
 [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
