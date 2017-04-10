---
title: "建立交易式發行集的可更新訂閱 (Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "07/21/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "可更新的交易式訂閱"
  - "可更新的交易式訂閱 SSMS"
ms.assetid: f9ef89ed-36f6-431b-8843-25d445ec137f
caps.latest.revision: 51
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 51
---
# 建立交易式發行集的可更新訂閱 (Management Studio)

> [!NOTE]  
>  這項功能在 [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] 2012 到 2016 的版本中仍然受到支援。  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
 
設定可更新的訂閱上 **可更新訂閱** 頁面 **新增訂閱精靈 」**。 此頁面僅在為可更新訂閱啟用了交易式發行集之後才可用。 如需啟用可更新訂閱的詳細資訊，請參閱 [啟用更新訂閱交易式發行集](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)。   
  
## 若要從發行者設定可更新訂閱  

1. 連接到 Microsoft SQL Server Management Studio 中的發行者，然後展開伺服器節點。

2. 展開 **[複寫]** 資料夾，然後展開 **[本機發行集]** 資料夾。

3. 交易式發行集啟用更新訂閱，請以滑鼠右鍵按一下，然後按一下 [ **新訂閱**。

4. 遵循精靈中的頁面來指定訂閱的選項，例如散發代理程式應在何處執行。

5. 在 **可更新訂閱** 頁面 **新增訂閱精靈 」**, ，確保 **複寫** 已選取。

6. 選取一個選項，從 **在發行者端認可** 下拉式清單︰

    * 若要使用立即更新訂閱，請選取 **同時認可變更**。 如果您選取此選項，且發行集允許佇列更新訂閱 （使用 「 新增發行集精靈 」 建立發行集的預設）、 訂閱屬性 **update_mode** 設為 **容錯移轉**。 如有必要，這個模式允許您以後可切換至佇列更新。

    * 若要使用佇列更新訂閱，請選取 **佇列變更且儘可能認可**。 如果您選取此選項，和發行集允許立即更新訂閱 （預設值建立新的發行集精靈 」 之發行集），而 「 訂閱者 」 正在執行 SQL Server 2005 或更新版本時，訂閱屬性 **update_mode** 設為已排入佇列的容錯移轉。 如有必要，這個模式允許您以後可切換至立即更新。

    如需切換更新模式的資訊，請參閱 [交換器之間更新模式可更新的交易式訂閱的](../../../relational-databases/replication/administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md)。

7. **可更新訂閱的登入** 頁面會顯示針對使用立即更新，或使用的訂閱 **update_mode** 設 **排入佇列的容錯移轉**。 在 **可更新訂閱的登入** 頁面上，指定連結的伺服器的連線到 「 發行者 」 會針對立即更新訂閱。 在訂閱者端引發的觸發程序，會使用這些連接將變更傳播至發行者。 選取下列其中一個選項：

    * **建立連結的伺服器會使用 SQL Server 驗證進行連接。** 若您已透過尚未定義遠端伺服器或訂閱者與發行者之間連結的伺服器，請選取此選項。 複寫會為您建立連結伺服器。 您必須指定已存在於發行者的帳戶。

    * **使用您已定義的連結伺服器或遠端伺服器。** 選取此選項，如果您已經定義遠端伺服器或 「 訂閱者 」 與 「 發行者 」 使用之間的連結的伺服器 [sp_addserver (TRANSACT-SQL)](../../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)，[sp_addlinkedserver (TRANSACT-SQL)](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md), ，SQL Server Management Studio 或另一種方法。

    連結的伺服器帳戶所需的權限的相關資訊，請參閱 **佇列更新訂閱的** 的 [輸入以下的連結描述](../../../relational-databases/replication/security/secure-the-subscriber.md)。

8. 完成精靈。

## 若要從訂閱者設定可更新訂閱


1. 連接到 SQL Server Management Studio，在訂閱者，然後展開伺服器節點。

2. 展開 **[複寫]** 資料夾。

3. 以滑鼠右鍵按一下 **本機訂閱** 資料夾，然後再按一下 **新訂閱**。

4. 在 **發行集** 頁面 **新增訂閱精靈 」**, ，請選取 **尋找 SQL Server 發行者** 從 **發行者** 下拉式清單。

5. 連接到 **[連接到伺服器]** 對話方塊中的發行者。

6. 選取 [交易式發行集啟用更新訂閱上 **發行集** 頁面。

7. 遵循精靈中的頁面來指定訂閱的選項，例如散發代理程式應在何處執行。

8. 在 **可更新訂閱** 頁面新增訂閱精靈 」 中，確定 **複寫** 已選取。

9. 選取一個選項，從 **在發行者端認可** 下拉式清單︰

    * 若要使用立即更新訂閱，請選取 **同時認可變更**。 如果您選取此選項，且發行集允許佇列更新訂閱 （使用 「 新增發行集精靈 」 建立發行集的預設）、 訂閱屬性 **update_mode** 設為 **容錯移轉**。 如有必要，這個模式允許您以後可切換至佇列更新。

    * 若要使用佇列更新訂閱，請選取 **佇列變更且儘可能認可**。 如果您選取此選項，和發行集允許立即更新訂閱 （預設值建立新的發行集精靈 」 之發行集），而 「 訂閱者 」 正在執行 SQL Server 2005 或更新版本時，訂閱屬性 **update_mode** 設為佇列 **容錯移轉**。 如有必要，這個模式允許您以後可切換至立即更新。

    如需切換更新模式的資訊，請參閱 [交換器之間更新模式可更新的交易式訂閱的](../../../relational-databases/replication/administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md)。

10. **可更新訂閱的登入** 頁面會顯示針對使用立即更新，或使用的訂閱 **update_mode** 設定為佇列 **容錯移轉**。 在 **可更新訂閱的登入** 頁面上，指定連結的伺服器的連線到 「 發行者 」 會針對立即更新訂閱。 在訂閱者端引發的觸發程序，會使用這些連接將變更傳播至發行者。 選取下列其中一個選項：

    * **建立連結的伺服器會使用 SQL Server 驗證進行連接。** 若您已透過尚未定義遠端伺服器或訂閱者與發行者之間連結的伺服器，請選取此選項。 複寫會為您建立連結伺服器。 您必須指定已存在於發行者的帳戶。

    * **使用您已定義的連結伺服器或遠端伺服器。** 選取此選項，如果您已經定義遠端伺服器或 「 訂閱者 」 與 「 發行者 」 使用之間的連結的伺服器 [sp_addserver (TRANSACT-SQL)](../../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)，[sp_addlinkedserver (TRANSACT-SQL)](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md), ，SQL Server Management Studio 或另一種方法。

    連結的伺服器帳戶所需的權限的相關資訊，請參閱 **佇列更新訂閱的** 的 [輸入以下的連結描述](../../../relational-databases/replication/security/secure-the-subscriber.md)。

11. 完成精靈。

## 另請參閱

[Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)

[Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)

[使用 Transact-SQL 建立交易式發行集的可更新訂閱](../../../relational-databases/replication/publish/create-updatable-subscription-to-transactional-publication.md) 
