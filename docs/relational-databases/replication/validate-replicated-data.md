---
title: "驗證複寫的資料 | Microsoft 文件"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- inline data validation [SQL Server replication]
- administering replication, validating data
- replication [SQL Server], validating data
- transactional replication, validating data
- validating data
- merge replication data validation [SQL Server replication]
- merge replication data validation [SQL Server replication], about data validation
- validating replicated data
ms.assetid: f7500a2b-61cb-41b5-816d-27609a6c58e7
caps.latest.revision: "45"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b9834f7c0d65ab05a7dda5f68b05438760abef21
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="validate-replicated-data"></a>驗證複寫的資料
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)] 異動與合併式複寫可以讓您驗證訂閱者端的資料是否與發行者端的資料相符。 可以驗證特定的訂閱或發行的所有訂閱。 指定下列其中一種驗證類型，「散發代理程式」或「合併代理程式」將在下次執行時驗證資料：  
  
-   僅限資料列計數。 這將會驗證「訂閱者」上的資料表與「發行者」上的資料表是否具有相同數量的資料列，但無法驗證資料列內容是否相符。 資料列計數驗證提供一種輕量型驗證方法，可讓您發現資料中的問題。  
  
-   資料列計數與二進位總和檢查碼。 除了統計「發行者」與「訂閱者」上的資料列數量之外，也會使用總和檢查碼演算法計算所有資料的總和檢查碼。 如果資料列計數失敗，就不會執行總和檢查碼。  
  
 除驗證「訂閱者」與「發行者」上的資料是否相符外，合併代理程式還可以驗證是否為每個「訂閱者」正確分割資料。 如需詳細資訊，請參閱[驗證合併訂閱者的資料分割資訊](../../relational-databases/replication/validate-partition-information-for-a-merge-subscriber.md)。  
  
 **若要驗證資料**  
  
 若要驗證訂閱中的所有發行項，請使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、預存程序或 Replication Management Objects (RMO)。 如需詳細資訊，請參閱 [Validate Data at the Subscriber](../../relational-databases/replication/validate-data-at-the-subscriber.md)。 若要驗證快照式和交易式發行集中的個別發行項，您必須使用預存程序。  
  
## <a name="data-validation-results"></a>資料驗證結果  
 當驗證完成時，「散發代理程式」或「合併代理程式」將記錄有關成功或失敗的訊息 (複寫不會報告具體是哪些資料列失敗)。 可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、「複寫監視器」和複寫系統資料表中檢視這些訊息。 以上列出的「如何」主題示範如何執行驗證並檢視結果。  
  
 若要處理驗證失敗，請考慮下列各項：  
  
-   設定名稱為 **複寫: 訂閱者資料驗證失敗** 的複寫警示，以便通知您失敗的情況。 如需詳細資訊，請參閱[設定預先定義的複寫警示 &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/administration/configure-predefined-replication-alerts-sql-server-management-studio.md)。  
  
-   您的應用程式是否有驗證失敗的問題？ 如果有驗證失敗的問題，請手動更新資料以便對其進行同步處理，或重新初始化訂閱：  
  
    -   可以使用 [tablediff 公用程式](../../tools/tablediff-utility.md)更新資料。 如需使用此公用程式的詳細資訊，請參閱[比較複寫資料表的差異 &#40;複寫程式設計&#41;](../../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md)。  
  
    -   如需詳細資訊，請參閱[重新初始化訂閱](../../relational-databases/replication/reinitialize-subscriptions.md)。  
  
## <a name="considerations-for-data-validation"></a>資料驗證的考量  
 在驗證資料時，請考慮下列問題：  
  
-   您必須在驗證資料之前停止「訂閱者」上的所有更新活動 (在進行驗證時不必停止「發行者」上的活動)。  
  
-   由於總和檢查碼與二進位總和檢查碼在驗證大型資料集時，可能需要使用大量的處理器資源，因此應該將驗證排在伺服器複寫活動最少的時間來進行。  
  
-   複寫僅驗證資料表；它無法驗證只有結構描述的發行項 (例如預存程序) 在「發行者」與「訂閱者」上是否相同。  
  
-   二進位總和檢查碼可以與任何已發行資料表一起使用。 總和檢查碼無法驗證具有資料行篩選或其中資料行位移不同 (由於 ALTER TABLE 陳述式卸除或新增資料行) 的邏輯資料表結構的資料表。  
  
-   複寫驗證會使用 **checksum** 和 **binary_checksum** 函數。 如需其行為的資訊，請參閱[總和檢查碼 &#40;Transact-SQL&#41;](../../t-sql/functions/checksum-transact-sql.md) 和 [BINARY_CHECKSUM  &#40;Transact-SQL&#41;](../../t-sql/functions/binary-checksum-transact-sql.md)。  
  
-   如果「訂閱者」與「發行者」端的資料類型不同，則使用二進位總和檢查碼或總和檢查碼的驗證可能會誤報失敗。 如果執行下列任何一項作業，就可能發生上述情況：  
  
    -   將結構描述選項明確地設定為對應舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的資料類型。  
  
    -   將合併式發行集的發行集相容性層級設定為舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，而已發行的資料表則包含一或多個必須對應此版本的資料類型。  
  
    -   手動初始化訂閱且在「訂閱者」端使用不同的資料類型。  
  
-   異動複寫的可轉換訂閱不支援二進位總和檢查碼與總和檢查碼驗證。  
  
-   複寫給非「[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者」的資料不支援驗證。  
  
## <a name="how-data-validation-works"></a>資料驗證如何運作  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 藉由計算「發行者」的資料列計數或總和檢查碼，然後將那些值與「訂閱者」所計算的資料列計數或總和檢查碼相比較，以驗證其資料。 整個發行集資料表計算一個值，整個訂閱資料表也計算一個值，但是 **text**、 **ntext**或 **image** 資料行的資料不包含在其計算中。  
  
 在執行計算時，會暫時以共用鎖定來鎖定正在執行資料列計數或總和檢查碼的資料表，但此計算會迅速完成，並移除共用鎖定，通常只需要數秒鐘。  
  
 使用二進位總和檢查碼時，資料行會逐一發生 32 位元的 Redundancy Check (CRC)，而不是資料頁中實際資料列的 CRC。 如此可讓具有該資料表的資料行在資料頁以任何次序排序，而仍可計算資料列的相同 CRC。 發行集具有資料列或資料行篩選時，可以使用二進位總和檢查碼驗證。  
  
## <a name="see-also"></a>另請參閱  
 [Best Practices for Replication Administration](../../relational-databases/replication/administration/best-practices-for-replication-administration.md)  
  
  
