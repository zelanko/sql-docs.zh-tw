---
title: 使用邏輯記錄分組相關資料列的變更
description: 了解如何使用 SQL Server 中的合併式複寫對相關資料列進行整體變更。
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication logical records [SQL Server replication]
- articles [SQL Server replication], logical records
- logical records [SQL Server replication]
ms.assetid: ad76799c-4486-4b98-9705-005433041321
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: da2699b397d7c5440adc9cdddb3e2b4c1b239fe7
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2020
ms.locfileid: "91867001"
---
# <a name="group-changes-to-related-rows-with-logical-records"></a>使用邏輯記錄分組相關資料列的變更
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 依預設，合併式複寫會按資料列逐一處理資料變更。 這適用於很多情況，但對於某些應用程式，有必要將相關資料列做為一個單位進行處理。 合併式複寫的邏輯記錄功能可讓您定義不同資料表中相關資料列之間的關聯性，以便將這些資料列做為一個單位進行處理。  
  
> [!NOTE]  
>  邏輯記錄功能可以獨立使用，也可以與聯結篩選結合使用。 如需聯結篩選的詳細資訊，請參閱＜ [Join Filters](../../../relational-databases/replication/merge/join-filters.md)＞。 若要使用邏輯記錄，發行集的相容性層級必須至少為 90RTM。  
  
 設想有以下三個相關資料表：  
  
 ![三個資料表邏輯記錄，只具有資料行名稱](../../../relational-databases/replication/merge/media/logical-records-01.gif "三個資料表邏輯記錄，只具有資料行名稱")  
  
 在此關聯性中， **Customers** 資料表為父資料表，具有一個主索引鍵資料行 **CustID**。 **Orders** 資料表有一個主索引鍵資料行 **OrderID**，且 **CustID** 資料行上存在外部索引鍵條件約束 (參考 **Customers** 資料表中的 **CustID** 資料行)。 同樣地， **OrderItems** 資料表也具有一個主索引鍵資料行 **OrderItemID**，且 **OrderID** 資料行上存在外部索引鍵條件約束 (參考到 **Orders** 資料表中的 **OrderID** 資料行)。  
  
 在此範例中，邏輯記錄是由 **Orders** 資料表中與單一 **CustID** 值相關的所有資料列以及 **OrderItems** 資料表中與 **Orders** 資料表中那些資料列相關的所有資料列所組成。 下圖顯示 Customer2 之邏輯記錄在三個資料表中的所有資料列：  
  
 ![具有值的三個資料表邏輯記錄](../../../relational-databases/replication/merge/media/logical-records-02.gif "具有值的三個資料表邏輯記錄")  
  
 若要定義發行項之間的邏輯記錄關聯性，請參閱＜ [定義合併資料表發行項之間的邏輯記錄關聯性](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md)＞。  
  
## <a name="benefits-of-logical-records"></a>邏輯記錄的優點  
 邏輯記錄功能具有兩個主要的優點：  
  
-   將資料變更做為一個單位。  
  
-   對多個資料表中的多個資料列同時進行衝突偵測和解決。  
  
### <a name="the-application-of-changes-as-a-unit"></a>將變更當做一個單位  
 如果合併處理中斷 (例如出現連接被卸除)，則在使用了邏輯記錄的情況下，部分完成的那組相關複寫變更會回復。 例如存在以下情況，「訂閱者」新增了一個新訂單 ( **OrderID** = 6)，並在 **OrderItems** 資料表中新增了兩個新的資料列，即 **OrderID** = 6，其 **OrderItemID** = 10， **OrderItemID** = 11。  
  
 ![具有值的三個資料表邏輯記錄](../../../relational-databases/replication/merge/media/logical-records-04.gif "具有值的三個資料表邏輯記錄")  
  
 如果複寫處理在 **OrderID** = 6 的 **Orders** 資料列完成後，但在 **OrderItems** 10 和 11 完成之前中斷，並且未使用邏輯記錄，則 **OrderID** = 6 的 **OrderTotal** 值將與 **OrderItems** 資料列之 **OrderAmount** 值的總和不一致。 如果使用了邏輯記錄， **OrderID** = 6 的 **Orders** 資料列不會得到認可，直至複寫了相關的 **OrderItems** 變更。  
  
 另一個實例中，如果使用了邏輯記錄，且當合併處理套用變更時，尚有人在查詢資料表，則使用者將看不到僅部分複寫的變更，直至它們全部完成。 例如，複寫處理上傳了 **OrderID** = 6 的 Orders 資料列，但有使用者在複寫處理對 **OrderItems** 資料列進行複寫之前查詢資料表，則 **OrderTotal** 值將與 **OrderAmount** 值之總和不相同。 如果使用了邏輯記錄，則在 **OrderItems** 資料列的處理完成，且交易做為一個單位得到認可之前，使用者將看不到 **Orders** 資料列。  
  
### <a name="the-application-of-conflict-handling-to-more-than-one-table"></a>對多個資料表的衝突處理  
 設想有兩個「訂閱者」包含上述資料設定的情況：  
  
-   第一個「訂閱者」端的使用者將 **OrderItemID** 5 的 **OrderAmount** 從 100 變更到 150，將 **OrderID** 3 的 **OrderTotal** 從 200 變更到 250。  
  
-   第二個「訂閱者」端的使用者將 **OrderItemID** 6 的 **OrderAmount** 從 25 變更到 125，將 **OrderID** 3 的 **OrderTotal** 從 200 變更到 300。  
  
 如果這些變更在未使用邏輯記錄的情況下進行了複寫，則不同的 **OrderTotal** 值會造成衝突，且僅會複寫它們中的一個。 但是 **OrderItems** 資料表中的不衝突變更會在沒有衝突的情況下進行複寫，使最終的 **OrderTotal** 值與 **OrderItems** 資料列處於不一致的狀態。 如果在此實例中使用了邏輯記錄，與失敗的 **Orders** 資料表變更相關聯的 **OrderItems** 變更也會被回復，且最終的 **OrderTotal** 值會是 **OrderItems** 資料列的精確總和。  
  
 如需邏輯記錄衝突偵測和解決方法相關選項的詳細資訊，請參閱[偵測和解決邏輯記錄中的衝突](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-resolving-in-logical-record.md)。  
  
## <a name="considerations-for-using-logical-records"></a>使用邏輯記錄的考量  
 使用邏輯記錄時，請記住下列考量。  
  
### <a name="general-considerations"></a>一般考量  
  
-   建議盡可能減少邏輯記錄中的資料表數；建議五個或更少。  
  
-   邏輯記錄無法參考含下列資料類型的資料行：  
  
    -   **varchar(max)** 及 **nvarchar(max)**  
  
    -   **varbinary(max)**  
  
    -   **text** 及 **ntext**  
  
    -   **image**  
  
    -   **XML**  
  
    -   **UDT**  
  
-   已發行資料表中的外部索引鍵關聯性無法使用 CASCADE 選項進行定義。 如需詳細資訊，請參閱 [CREATE TABLE &#40;Transact-SQL&#41;](../../../t-sql/statements/create-table-transact-sql.md) 和 [ALTER TABLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-table-transact-sql.md)。  
  
-   無法更新邏輯關聯性子句中使用的任何資料行。  
  
-   對於邏輯記錄中包含的發行項，不支援使用商務邏輯處理常式或自訂解析程式進行自訂衝突解決。  
  
-   如果在包含了參數化篩選的發行集中使用邏輯記錄，您必須使用「訂閱者」資料分割的快照集來初始化「訂閱者」。 如果您使用其他方法初始化「訂閱者」，「合併代理程式」將失敗。 如需詳細資訊，請參閱 [Snapshots for Merge Publications with Parameterized Filters](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)。  
  
-   「衝突檢視器」中不會顯示涉及邏輯記錄的衝突。 若要檢視這些衝突的相關資訊，請使用複寫預存程序。 如需詳細資訊，請參閱[檢視合併式發行集的衝突資訊 &#40;複寫 Transact-SQL 程式設計&#41;](../view-and-resolve-data-conflicts-for-merge-publications.md)。  
  
### <a name="publication-settings"></a>發行集設定  
  
-   發行集的相容性層級必須為 90RTM 或更高。 如需詳細資訊，請參閱[複寫回溯相容性](../../../relational-databases/replication/replication-backward-compatibility.md)中的＜發行集相容性層級＞一節。  
  
-   發行集必須使用原生快照集模式。 此為預設值，除非您要複寫到不支援邏輯記錄的 [!INCLUDE[ssEW](../../../includes/ssew-md.md)]。  
  
-   發行集不允許 Web 同步處理。 如需有關 Web 同步處理的詳細資訊，請參閱＜ [Web Synchronization for Merge Replication](../../../relational-databases/replication/web-synchronization-for-merge-replication.md)＞。  
  
-   為了在篩選的發行集中使用邏輯記錄：  
  
    -   必須同時使用預先計算資料分割。 對預先計算資料分割的要求也同樣適用於邏輯記錄。 如需詳細資訊，請參閱[使用預先計算的資料分割最佳化參數化篩選效能](../../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)。  
  
    -   無法使用不重疊的參數化篩選。 如需詳細資訊，請參閱＜ [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)＞的「設定資料分割選項」一節。  
  
-   如果發行集使用聯結篩選，則對於邏輯記錄關聯性中涉及的所有聯結篩選，其 **聯結唯一索引鍵** 屬性都必須設定為 **true** 。 如需相關資訊，請參閱 [Join Filters](../../../relational-databases/replication/merge/join-filters.md)。  
  
### <a name="relationships-between-tables"></a>資料表之間的關聯性  
  
-   透過邏輯記錄相關聯的資料表必須具有主索引鍵與外部索引鍵的關聯性。  
  
-   無法為外部索引鍵條件約束設定 NOT FOR REPLICATION 選項。  
  
-   多個子資料表可以只有一個父資料表。  
  
     例如，追蹤班級和學生的資料庫設計可能類似於：  
  
     ![具有超過一個父系資料表的子系資料表](../../../relational-databases/replication/merge/media/logical-records-03.gif "具有超過一個父系資料表的子系資料表")  
  
     無法使用邏輯記錄來代表此關聯性中的三個資料表，因為 **ClassMembers** 中的資料列並未與單一主索引鍵資料列相關聯。 資料表 **Classes** 和 **ClassMembers** 仍然可以組成邏輯記錄，資料表 **ClassMembers** 和 **Students**也可以，但是三個資料表一起則不行。  
  
-   發行集不能包含循環聯結篩選關聯性。  
  
     以包含資料表 **Customers**、 **Orders**和 **OrderItems**為例，如果 **Orders** 資料表同樣具有參考到 **OrderItems** 資料表的外部索引鍵條件約束，則無法使用邏輯記錄。  
  
## <a name="performance-implications-of-logical-records"></a>邏輯記錄的效能含意  
 邏輯記錄功能會帶來效能成本。 如果不使用邏輯記錄，複寫代理程式可以同時處理給定發行項的所有變更，同時由於變更會按資料列逐一套用，因此套用變更所需的鎖定及交易記錄檔要求便最小。  
  
 如果使用邏輯記錄，「合併代理程式」必須同時處理各完整邏輯記錄的變更。 這會影響「合併代理程式」複寫資料列所需的時間。 此外，由於代理程式會為每個邏輯記錄單獨開啟一個交易，因此鎖定的要求也會增加。  
  
## <a name="see-also"></a>另請參閱  
 [合併式複寫的發行項選項](../../../relational-databases/replication/merge/article-options-for-merge-replication.md)  
  
