---
title: Create an Updatable Subscription to a Transactional Publication (Management Studio) |Microsoft Docs
ms.custom: ''
ms.date: 07/20/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- SQL Server 2014
helpviewer_keywords:
- updateable transactional subscriptions
- updateable transactional subscriptions, SSMS
ms.assetid: f9ef89ed-36f6-431b-8843-25d445ec137f
caps.latest.revision: 46
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1b6a3e276eb1250938e882316f84cf61f49a5b7e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37290464"
---
# <a name="create-an-updatable-subscription-to-a-transactional-publication-management-studio"></a>建立交易式發行集的可更新訂閱 (Management Studio)

> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
 
在 [新增訂閱精靈] 的 [可更新訂閱] 頁面上設定可更新訂閱。 此頁面僅在為可更新訂閱啟用了交易式發行集之後才可用。 如需啟用可更新訂閱的詳細資訊，請參閱[啟用交易式發行集的可更新訂閱](enable-updating-subscriptions-for-transactional-publications.md)。   
  
## <a name="to-configure-an-updatable-subscription-from-the-publisher"></a>若要從發行者設定可更新訂閱  

1. 連線到 Microsoft SQL Server Management Studio 中的發行者，然後展開伺服器節點。

2. 展開 **[複寫]** 資料夾，然後展開 **[本機發行集]** 資料夾。

3. 以滑鼠右鍵按一下為更新訂閱啟用的交易式發行集，然後按一下 [新增訂閱]。

4. 遵循精靈中的頁面來指定訂閱的選項，例如散發代理程式應在何處執行。

5. 在 [新增訂閱精靈] 的 [可更新的訂閱] 頁面上，確定已選取 [複寫]。

6. 從 [在發行者端認可] 下拉式清單中選取一個選項：

    * 若要使用立即更新訂閱，請選取 [同時認可變更]。 如果您選取這個選項，而且發行集允許佇列更新訂閱 (使用 [新增發行集精靈] 所建立之發行集的預設值)，訂閱屬性 **update_mode** 會設定為 **failover**。 如有必要，這個模式允許您以後可切換至佇列更新。

    * 若要使用佇列更新訂閱，請選取 [佇列變更且盡可能認可]。 如果您選取這個選項，而發行集允許立即更新訂閱 (使用 [新增發行集精靈] 建立之發行集的預設值)，而且訂閱者執行的是 SQL Server 2005 或更新版本，則訂閱屬性 **update_mode** 會設定為 queued failover。 如有必要，這個模式允許您以後可切換至立即更新。

    如需切換更新模式的資訊，請參閱[切換可更新之交易式訂閱的更新模式](../administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md)。

7. 針對使用立即更新或將 **update_mode** 設定為 **queued failover**，會顯示 [可更新訂閱的登入] 頁面。 在 [可更新訂閱的登入] 頁面上，指定連線到發行者之連結的伺服器，以立即更新訂閱。 在訂閱者端引發的觸發程序，會使用這些連接將變更傳播至發行者。 選取下列其中一個選項：

    * **建立使用 SQL Server 驗證來連線的連結伺服器。** 若您已透過尚未定義遠端伺服器或訂閱者與發行者之間連結的伺服器，請選取此選項。 複寫會為您建立連結伺服器。 您必須指定已存在於發行者的帳戶。

    * **使用您已定義的連結伺服器或遠端伺服器。** 若您已透過 [sp_addserver (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addserver-transact-sql)、[sp_addlinkedserver (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql)、SQL Server Management Studio 或其他方法定義遠端伺服器或訂閱者與發行者之間連結的伺服器，請選取此選項。

    如需連結伺服器帳戶所需權限的資訊，請參閱[在這裡輸入連結描述](../security/secure-the-subscriber.md)的**佇列更新訂閱**。

8. 完成精靈。

## <a name="to-configure-an-updatable-subscription-from-the-subscriber"></a>若要從訂閱者設定可更新訂閱


1. 連線到 SQL Server Management Studio 中的訂閱者，然後展開伺服器節點。

2. 展開 **[複寫]** 資料夾。

3. 以滑鼠右鍵按一下 **[區域訂閱]** 資料夾，然後按一下 **[新增訂閱]**。

4. 在 [新增訂閱精靈] 的 [發行集] 頁面上，從 [發行者] 下拉式清單中選取 [<尋找 SQL Server 發行者>]。

5. 連接到 **[連接到伺服器]** 對話方塊中的發行者。

6. 在 [發行集] 頁面上選取為更新訂閱啟用的交易式發行集。

7. 遵循精靈中的頁面來指定訂閱的選項，例如散發代理程式應在何處執行。

8. 在 [新增訂閱精靈] 的 [可更新的訂閱] 頁面上，確定已選取 [複寫]。

9. 從 [在發行者端認可] 下拉式清單中選取一個選項：

    * 若要使用立即更新訂閱，請選取 [同時認可變更]。 如果您選取這個選項，而且發行集允許佇列更新訂閱 (使用 [新增發行集精靈] 所建立之發行集的預設值)，訂閱屬性 **update_mode** 會設定為 **failover**。 如有必要，這個模式允許您以後可切換至佇列更新。

    * 若要使用佇列更新訂閱，請選取 [佇列變更且盡可能認可]。 如果您選取這個選項，而發行集允許立即更新訂閱 (使用 [新增發行集精靈] 建立之發行集的預設值)，而且訂閱者執行的是 SQL Server 2005 或更新版本，則訂閱屬性 **update_mode** 會設定為 **queued failover**。 如有必要，這個模式允許您以後可切換至立即更新。

    如需切換更新模式的資訊，請參閱[切換可更新之交易式訂閱的更新模式](../administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md)。

10. 針對使用立即更新或將 **update_mode** 設定為 **queued failover**，會顯示 [可更新訂閱的登入] 頁面。 在 [可更新訂閱的登入] 頁面上，指定連線到發行者之連結的伺服器，以立即更新訂閱。 在訂閱者端引發的觸發程序，會使用這些連接將變更傳播至發行者。 選取下列其中一個選項：

    * **建立使用 SQL Server 驗證來連線的連結伺服器。** 若您已透過尚未定義遠端伺服器或訂閱者與發行者之間連結的伺服器，請選取此選項。 複寫會為您建立連結伺服器。 您必須指定已存在於發行者的帳戶。

    * **使用您已定義的連結伺服器或遠端伺服器。** 若您已透過 [sp_addserver (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addserver-transact-sql)、[sp_addlinkedserver (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql)、SQL Server Management Studio 或其他方法定義遠端伺服器或訂閱者與發行者之間連結的伺服器，請選取此選項。

    如需連結伺服器帳戶所需權限的資訊，請參閱[在這裡輸入連結描述](../security/secure-the-subscriber.md)的**佇列更新訂閱**。

11. 完成精靈。

## <a name="see-also"></a>另請參閱

[Updatable Subscriptions for Transactional Replication](../transactional/updatable-subscriptions-for-transactional-replication.md)

[Create a Publication](create-a-publication.md)

[使用 Transact-SQL 建立交易式發行集的可更新訂閱](../create-updatable-subscription-transactional-publication-transact-sql.md) 
 
  
