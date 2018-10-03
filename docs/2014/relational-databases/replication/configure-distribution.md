---
title: 設定散發 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], distribution
- distribution configuration [SQL Server replication]
- remote Distributors [SQL Server replication]
- transactional replication, configuring distribution
- distribution databases [SQL Server replication], sizing
- Distributors [SQL Server replication], configuring
- distribution databases [SQL Server replication], about distribution databases
- distribution databases [SQL Server replication]
- merge replication [SQL Server replication], configuring distribution
ms.assetid: 94d52169-384e-4885-84eb-2304e967d9f7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 794a5097e78c8a77bba8a6c5d37f49020372c88f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48202758"
---
# <a name="configure-distribution"></a>設定散發
  「散發者」是包含散發資料庫的伺服器，該資料庫會存儲所有類型之複寫的中繼資料和記錄資料，以及異動複寫的交易。 若要設定複寫，您必須設定「散發者」。 每個「發行者」可以僅指派給一個「散發者」執行個體，但是多個發行者可以共用一個「散發者」。 散發者會使用所在伺服器的下列額外資源：  
  
-   如果發行集的快照集檔案儲存於「散發者」(通常如此) 時，則使用額外的磁碟空間。  
  
-   儲存散發資料庫的額外空間。  
  
-   針對在散發者上執行的發送訂閱，複寫代理程式會使用額外處理器資源。  
  
 您選擇作為散發者的伺服器，應該具備足夠的磁碟空間及處理器動力，以便支援該伺服器的複寫及所有其他活動。 在您設定「散發者」時，需指定下列項目：  
  
-   快照集資料夾，依預設，該資料夾用於所有使用此「散發者」的「發行者」。 確定此資料夾已共用，並已設定適當的權限。 如需詳細資訊，請參閱[保護快照集資料夾](security/secure-the-snapshot-folder.md)。  
  
-   散發資料庫的名稱和檔案位置。 散發資料庫建立後，不能重新命名。 若要使用不同的資料庫名稱，則必須停用散發並對它進行重新設定。  
  
-   任何授權使用「散發者」的「發行者」。 如果指定「發行者」，而不是「散發者」執行的執行個體，則還必須指定「發行者」連接到遠端「散發者」的密碼。  
  
 對於異動複寫，在設定散發之後，我們建議您：  
  
-   適當調整散發資料庫的大小。 用一般負載量為系統測試複寫，以決定需要多少空間儲存命令。 確認資料庫大小足夠儲存命令，且無須經常自動成長。 如需變更資料庫大小的詳細資訊，請參閱 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)。  
  
-   在散發資料庫設定 **sync with backup** 選項。 如需詳細資訊，請參閱[備份與還原快照式和異動複寫的策略](administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md)和[為異動複寫啟用協調備份 &#40;複寫 Transact-SQL 程式設計&#41;](administration/enable-coordinated-backups-for-transactional-replication.md)。  
  
## <a name="local-and-remote-distributors"></a>本機與遠端散發者  
 依預設，「散發者」可以和「發行者」(本機「散發者」) 為相同伺服器，也可以和「發行者」(遠端「散發者」) 為不同伺服器。 如果您要執行下列項目，通常要選擇使用遠端「散發者」：  
  
-   如果您想使來自「發行者」上的複寫之影響為最小 (例如，如果「發行者」為 OLTP 伺服器)，則將處理卸載到其他電腦。  
  
-   為多個發行者設定集中化散發者  
  
 由於下列兩個原因，遠端「散發者」在異動複寫中比在合併式複寫中更為常見：  
  
-   「散發者」在異動複寫中扮演更重要的角色，因為所有複寫的交易會寫入散發資料庫，並從中讀取。  
  
-   合併式複寫拓撲通常使用提取訂閱，所以代理程式會在每個「訂閱者」端執行，而不是在「散發者」端執行。 如需詳細資訊，請參閱[訂閱發行集](subscribe-to-publications.md)。 在大多數情況下，您應將使用合併式複寫的本機「散發者」。  
  
 若要設定發行和散發，請參閱＜ [Configure Publishing and Distribution](configure-publishing-and-distribution.md)＞。  
  
 若要修改發行者和散發者屬性，請參閱＜ [View and Modify Distributor and Publisher Properties](view-and-modify-distributor-and-publisher-properties.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [發行資料和資料庫物件](publish/publish-data-and-database-objects.md)   
 [保護散發者](security/secure-the-distributor.md)  
  
  
