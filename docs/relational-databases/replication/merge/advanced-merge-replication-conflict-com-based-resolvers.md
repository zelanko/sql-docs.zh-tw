---
title: "以 Microsoft COM 為基礎的解析程式 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- COM-based resolvers [SQL Server replication]
- custom resolvers [SQL Server replication]
ms.assetid: a6637e4b-4e6b-40aa-bee6-39d98cc507c8
caps.latest.revision: "38"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 01b82214e9d862bcd12b031a6cea6184a48ddabb
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="advanced-merge-replication-conflict---com-based-resolvers"></a>進階合併式複寫衝突 - 以 COM 為基礎的解析程式
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 提供的所有以 COM 為基礎的解決器可處理更新衝突，如有需要，也可以處理插入與刪除衝突。 它們都能處理資料行追蹤，大部分還能處理資料列追蹤。 這些及所有其他的以 COM 為基礎的解決器都宣告它們所能處理的衝突類型，而「合併代理程式」使用預設解決器來處理其他所有的衝突類型。  
  
 解決器在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的安裝過程中安裝。 執行 **sp_enumcustomresolvers** 預存程序以檢視電腦中註冊的所有衝突解決器。 執行該程序，可顯示個別結果集中各解決器的描述和全域唯一識別碼 (GUID)。  
  
 若要指定解析程式，請參閱＜ [Specify a Merge Article Resolver](../../../relational-databases/replication/publish/specify-a-merge-article-resolver.md)＞。  
  
 下表說明了各解決器的屬性。  
  
|名稱|必要輸入|說明|註解|  
|----------|--------------------|-----------------|--------------|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 相加衝突解決器|要加總的資料行名稱。 它必須要有算術資料類型 (例如 **int**、 **smallint**、 **numeric**，等等)。|衝突成功者是由優先權值決定的。 指定設定為來源與目的地資料行值總和的資料行值。 如果其中有一個資料行設為 NULL，則結果資料行值即被設為另一資料行的值。|支援更新衝突，僅限資料行追蹤。|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 平均衝突解決器|要取平均值的資料行名稱。 它必須要有算術資料類型 (例如 **int**、 **smallint**、 **numeric**，等等)。|衝突成功者是由優先權值決定的。 結果資料行值設定為來源與目的地資料行值的平均值。 如果其中有一個資料行設為 NULL，則結果資料行值即被設為另一資料行的值。|支援更新衝突，僅限資料行追蹤。|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] DATETIME (取時間較早者) 衝突解決器|要用來決定衝突成功者的資料行名稱。 它必須具有 **datetime** 資料類型。|具有較早 **datetime** 值的資料行決定衝突成功者。 如果其中有一個資料行設為 NULL，則含有另一資料行的資料列便是成功者。|支援更新衝突、資料列與資料行追蹤。 資料行值直接進行比較，且不會依不同時區進行調整。|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] DATETIME (取時間較晚者) 衝突解決器|要用來決定衝突成功者的資料行名稱。 它必須具有 **datetime** 資料類型。|具有較晚 **datetime** 值的資料行決定衝突成功者。 如果其中有一個資料行設為 NULL，則含有另一資料行的資料列便是成功者。|支援更新衝突、資料列與資料行追蹤。|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 最大值衝突解決器|要用來決定衝突成功者的資料行名稱。 它必須要有算術資料類型 (例如 **int**、 **smallint**、 **numeric**，等等)。|具有較大數值的資料行決定衝突成功者。 如果其中有一個資料行設為 NULL，則含有另一資料行的資料列便是成功者。|支援資料列與資料行追蹤。|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 最小值衝突解決器|要用來決定衝突成功者的資料行名稱。 它必須要有算術資料類型 (例如 **int**、 **smallint**、 **numeric**，等等)。|具有較小數值的資料行決定衝突成功者。 如果其中有一個資料行設為 NULL，則含有另一資料行的資料列便是成功者。|支援更新衝突，資料列和資料行的追蹤。|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 合併文字衝突解決器|文字資料行與分隔符號的名稱，例如 `@resolver_info = '[col1][===]'`。|衝突成功者是由優先權值決定的。 衝突中的文字資料行設定為合併值，包含通用前置詞，後面接著「發行者」的唯一部分，然後是分隔符號，最後是「訂閱者」的唯一部分。|支援更新衝突，僅限資料行追蹤。|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 一律取訂閱者衝突解決器|無輸入。|無論是來源或目的地，「訂閱者」都是成功者。|支援所有衝突類型。|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 優先順序資料行解決器|要用來決定衝突成功者的資料行名稱。 它必須要有算術資料類型 (例如 **int**、 **smallint**、 **numeric**，等等)。|具有較大數值的資料行決定衝突成功者。 如果其中有一個資料行設為 NULL，則含有另一資料行的資料列便是成功者。|支援更新衝突，資料列和資料行的追蹤。|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 僅上傳衝突解決器|無輸入。|接受上傳至「發行者」的變更；變更無法下載至「訂閱者」。|支援所有衝突類型。|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 僅下載衝突解決器|無輸入。|拒絕上傳至「發行者」的變更；變更可下載至「訂閱者」。|支援所有衝突類型。|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQL Server 預存程序解析程式|解決器應呼叫預存程序的名稱來處理衝突。|衝突解決方案視您在預存程序中指定的邏輯而定。|支援更新衝突。 如需詳細資訊，請參閱[針對合併發行項實作自訂衝突解析程式](../../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md)|  
  
## <a name="see-also"></a>另請參閱  
 [Advanced Merge Replication Conflict Detection and Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [sp_enumcustomresolvers &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md)  
  
  
