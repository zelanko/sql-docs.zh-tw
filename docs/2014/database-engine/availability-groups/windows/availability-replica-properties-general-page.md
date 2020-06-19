---
title: 可用性複本屬性 (一般頁面) | Microsoft Docs
ms.custom: ''
ms.date: 10/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilityreplicaproperties.general.f1
ms.assetid: 8318fefb-e045-4fab-8507-e1951fc7cec6
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: fb7e75fd1e25d8f4089d14688096afd0aa4dea8d
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84937031"
---
# <a name="availability-replica-properties-general-page"></a>可用性複本屬性 (一般頁面)
  使用此對話方塊來檢視可用性複本的屬性。  
  
## <a name="task-list"></a>工作清單  
 **若要檢視可用性複本屬性**  
  
-   [檢視可用性複本屬性 &#40;SQL Server&#41;](view-availability-replica-properties-sql-server.md)  
  
-   [使用 AlwaysOn 儀表板 &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
## <a name="ui-element-list"></a>UI 元素清單  
 **可用性群組名稱**  
 可用性群組的名稱。 這是使用者指定的名稱，它在 Windows Server 容錯移轉叢集 (WSFC) 內必須是唯一的。  
  
 **伺服器執行個體**  
 裝載這個複本之 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的伺服器名稱，如果是非預設執行個體，則是它的執行個體名稱。  
  
 **角色**  
 **主要**  
 目前的主要複本。  
  
 **次要**  
 目前的次要複本。  
  
 **解析中**  
 複本角色目前正在解析成主要或次要角色。  
  
 **可用性模式**  
 複本的可用性模式，下列其中一項：  
  
 **非同步認可**  
 主要複本可認可交易，而不需要等候次要複本將記錄寫入磁碟中。  
  
 **同步認可**  
 主要複本會等候認可給定交易，直到次要複本將交易寫入磁碟為止。  
  
 如需詳細資訊，請參閱[可用性模式（AlwaysOn 可用性群組）](availability-modes-always-on-availability-groups.md)。  
  
 **容錯移轉模式**  
 複本的容錯移轉模式，下列其中一項：  
  
 **自動**  
 自動容錯移轉。 此複本是自動容錯移轉的目標。 只有當可用性模式設定為同步認可時，才支援這個選項。  
  
 **手動**  
 手動容錯移轉。 此複本只能由資料庫管理員手動容錯移轉。  
  
 **主要角色中的連接**  
 當複本擁有主要角色時所支援的用戶端連接類型。  
  
 **允許所有連接**  
 主要複本的資料庫允許所有連接。 這是預設值。  
  
 **允取讀取/寫入連接**  
 不允許 Application Intent 連接屬性設為 **ReadOnly** 的連接。 當 [應用程式意圖] 屬性設定為 [ **ReadWrite** ]，或未設定 [應用程式意圖連接] 屬性時，就會允許連接。  
  
 **可讀取次要**  
 執行次要角色的可用性複本 (也就是次要複本) 是否可接受來自用戶端的連接，下列其中一個值：  
  
 **否**  
 不允許直接連接這個複本的次要資料庫。 無法讀取這些資料庫。 這是預設值。  
  
 **僅限讀取意圖**  
 只允許與這個複本的次要資料庫進行直接唯讀連接。 可以讀取所有次要資料庫。  
  
 **是**  
 允許與這個複本的次要資料庫之間的所有連接，但只供讀取存取。 可以讀取所有次要資料庫。  
  
 如需詳細資訊，請參閱使用中[次要資料庫：可讀取的次要複本（AlwaysOn 可用性群組）](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)。  
  
 **會話超時（秒）**  
 逾時期間 (以秒為單位)。 逾時期間是將主要複本與次要複本之間的連接視為失敗之前，複本等待接收另一個複本之訊息的時間上限。 工作階段逾時會偵測次要複本是否連接到主要複本。 一旦偵測到與次要複本之間的連接失敗時，主要複本會將次要複本視為 NOT_SYNCHRONIZED。 一旦偵測到與主要複本之間的連接失敗時，次要複本只會嘗試重新連接。  
  
> [!NOTE]  
>  工作階段逾時不會造成自動容錯移轉。  
  
 **端點 URL**  
 使用者指定之資料庫鏡像端點的字串表示法，該端點是由主要與次要複本之間的資料同步處理連接所使用。 如需這些端點 URL 語法的相關資訊，請參閱[在加入或修改可用性複本時指定端點 URL &#40;SQL Server&#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md)。  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組 &#40;SQL Server 的總覽&#41;](overview-of-always-on-availability-groups-sql-server.md)  
  
  
