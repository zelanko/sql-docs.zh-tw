---
title: Stretch Database | Microsoft Docs
ms.custom: ''
ms.date: 06/27/2016
ms.prod: sql
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Stretch Database
ms.assetid: ce6db775-21a5-40bc-95a1-f560376d4ee2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4386963a4ca821b86e03129a958d38373aa3ecbe
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52503795"
---
# <a name="stretch-database"></a>Stretch Database
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  Stretch Database 以透明且安全的方式，將您的原始資料遷移到 Microsoft Azure 雲端。  
  
 如果您想要立即開始使用 Stretch Database，請參閱 [Get started by running the Enable Database for Stretch Wizard](../../sql-server/stretch-database/get-started-by-running-the-enable-database-for-stretch-wizard.md)。  
  
## <a name="what-are-the-benefits-of-stretch-database"></a>Stretch Database 有什麼優勢？  
 Stretch Database 提供下列優勢：  
  
 **為冷資料提供符合成本效益的可用性**  
 使用 SQL Server Stretch Database 以動態方式將暖交易資料和冷交易資料從 SQL Server 延展到 Microsoft Azure。 與一般冷資料儲存區不同的是，您的資料會一直在線上而且可供查詢。 您可以提供較長的資料保留時間軸，而不需要為「客戶訂單記錄」之類的大型資料表砸下大筆花費。 受益於低成本的 Azure，而不是調整昂貴的內部部署儲存體。 您可以在 Azure 入口網站選擇定價層並進行設定，以維持對定價及成本的控制。 視需要相應增加或減少。 如需詳細資料，請瀏覽 [SQL Server Stretch Database 定價](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/) 。  
  
 **不需要變更查詢或應用程式**  
 無論您的 SQL Server 資料位於內部部署或已延展到雲端，都能平順地存取。  您可以設定原則以決定資料的儲存位置，而 SQL Server 會在背景處理資料移動。 整個資料表都會一直在線上，而且可供查詢。 此外，因為資料位置對應用程式而言完全透明，所以 Stretch Database 不會要求對現有查詢或應用程式進行任何變更。  
  
 **簡化內部部署資料維護**  
 減少資料的內部部署維護與儲存。 內部部署資料的備份會執行得更快，並在維護時間窗口內完成。 資料的雲端部分備份會自動執行。 您的內部部署儲存需求將大幅減少。 Azure 儲存體的成本與加入內部部署 SSD 相比，可節省 80%。  
  
 **即使在移轉期間也能保護您的資料安全**  
 您可以安全地將最重要的應用程式延展到雲端，因此大可放心。 SQL Server 的 Always Encrypted 可為移動中的資料提供加密。 資料列層級安全性 (RLS) 及其他進階 SQL Server 安全性功能也可搭配 Stretch Database 運作，以保護您的資料。  
  
## <a name="what-does-stretch-database-do"></a>Stretch Database 有何作用？  
 當您對 SQL Server 執行個體、資料庫或選取至少一個資料表啟用 Stretch Database 後，Stretch Database 就會在幕後將您的原始資料移轉到 Azure。  
  
-   如果您將原始資料儲存在個別的資料表中，可以遷移整個資料表。  
  
-   若您的資料表同時包含作用及原始資料，您可以指定篩選函數，以選取要移轉的資料列。

**您不需要變更現有查詢及用戶端應用程式。** 即使在資料遷移期間，您仍然能夠順利存取本機和遠端資料。 遠端查詢會有少量延遲，但您只會在查詢原始資料時遇到這樣的延遲。

**Stretch Database 可確保在遷移期間發生錯誤時，也不會有任何資料遺失。** 其具有重試邏輯，可處理遷移期間可能發生的連線問題。 動態管理檢視會提供遷移狀態。

**您可以暫停資料遷移** ，以對本機伺服器的問題進行疑難排解，或將可用的網路頻寬最大化。  
  
 ![Stretch Database 概觀](../../sql-server/stretch-database/media/stretch-overview.png "Stretch Database 概觀")  
  
## <a name="is-stretch-database-for-you"></a>Stretch Database 適合您嗎？  
 如果您可以進行下列陳述式，Stretch Database 就能協助您滿足需求並解決問題。  
  
|如果您是決策者|如果您是 DBA|  
|--------------------------------|---------------------|  
|我必須長期保留交易資料。|我的資料表大小越來越難以控制。|  
|我有時需要查詢原始資料。|我的使用者表示他們想要存取原始資料，但很少會用到。|  
|我有不想更新的應用程式，包括較舊的應用程式。|我必須持續購買及新增更多儲存體。|  
|我想要找到節省儲存成本的方法。|我無法在 SLA 內備份或還原這類大型資料表。|  
  
## <a name="what-kind-of-databases-and-tables-are-candidates-for-stretch-database"></a>哪種資料庫和資料表是 Stretch Database 的對象？  
 Stretch Database 以包含大量原始資料的交易資料庫為目標，而這些資料通常儲存在少量資料表中。 這些資料表可能包含十億個以上的資料列。  
  
 如果您使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的時態表功能，請使用 Stretch Database 將所有或一部分相關記錄資料表遷移到 Azure 符合成本效益的儲存體。 如需詳細資訊，請參閱 [管理系統設定版本之時態表中的歷程記錄資料保留](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)。  
  
 請使用 SQL Server 2016 升級建議程式的功能 Stretch Database Advisor，為 Stretch Database 識別資料庫和資料表。 如需詳細資訊，請參閱 [執行 Stretch Database Advisor 以識別 Stretch Database 的資料庫和資料表](../../sql-server/stretch-database/stretch-database-databases-and-tables-stretch-database-advisor.md)。 若要深入了解潛在的封鎖問題，請參閱 [Stretch Database 的介面區限制和封鎖問題](../../sql-server/stretch-database/limitations-for-stretch-database.md)。  

## <a name="test-drive-stretch-database"></a>試用 Stretch Database  
 **透過 AdventureWorks 範例資料庫試用 Stretch Database。** 若要取得 AdventureWorks 範例資料庫，至少要從 [這裡](https://www.microsoft.com/download/details.aspx?id=49502)。 將範例資料庫還原到 SQL Server 2016 的執行個體後，請將範例檔案解壓縮，然後從 Stretch DB 資料夾開啟 Stretch DB 範例檔案。 執行此檔案中的指令碼，以檢查您的資料在啟用 Stretch Database 前後所使用的空間，進而追蹤資料遷移的進度，並確認您可在資料遷移期間和遷移後繼續查詢現有資料和插入新資料。  
  
## <a name="next-step"></a>下一步  
 **識別屬於 Stretch Database 對象的資料庫和資料表。** 下載 SQL Server 2016 升級建議程式，並執行 Stretch Database Advisor，識別屬於 Stretch Database 對象的資料庫和資料表。 Stretch Database Advisor 也可以識別封鎖問題。 如需詳細資訊，請參閱 [執行 Stretch Database Advisor 以識別 Stretch Database 的資料庫和資料表](../../sql-server/stretch-database/stretch-database-databases-and-tables-stretch-database-advisor.md)。  
  
  
