---
title: 使用原則式管理來管理伺服器 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- facet See facets
- Declarative Management Framework See Policy-Based Management
- surface area configuration [SQL Server], Policy-Based Management
- Policy-Based Management
- facets [Policy-Based Management]
- Policy-Based Management, administering
- conditions [Policy-Based Management]
- facets [Policy-Based Management], about facets
- PolicyAdministratorRole role
ms.assetid: ef2a7b3b-614b-405d-a04a-2464a019df40
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: c62c2372b0a61d0a09a0e15998f2340b995fc919
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68109929"
---
# <a name="administer-servers-by-using-policy-based-management"></a>使用原則式管理來管理伺服器
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
   原則式管理是用於管理一個或多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的原則式系統。 其用法是為了建立包含條件運算式的條件。 然後，建立將這些條件套用至資料庫目標物件的原則。  

例如，身為資料庫管理員，您可能想要確定特定伺服器未啟用 Database Mail，以便建立設定該伺服器選項的條件和原則。 
   
 > **重要！！** 原則可能會影響某些功能的運作方式。 例如，異動資料擷取和異動複寫都會使用沒有索引的 systranschemas 資料表。 如果您啟用了所有資料表都必須擁有索引的原則，則強制此原則的合規性將會造成這些功能失敗。  
  
 使用 SQL Server Management Studio 建立和管理原則，以執行下列動作：
  
1.  選取包含要設定之屬性的以原則為基礎的管理 Facet。  
  
2.  定義指定管理 Facet 狀態的條件。  
  
3.  定義包含此條件、可篩選目標集的其他條件及評估模式的原則。  
  
4.  檢查 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體是否符合此原則。  
  
 若為失敗的原則，[物件總管] 會指出嚴重健全狀況警告成為目標旁的紅色圖示以及 [物件總管] 樹狀結構中較高的節點。  
  
> **注意：** 當系統計算原則的物件集時，根據預設會排除系統物件。  例如，如果原則的物件集是指所有資料表，則原則不會套用至系統資料表。 如果使用者想要對系統物件評估原則，可以明確地將系統物件加入至物件集。 不過，雖然 **check on schedule** 評估模式支援所有原則，但基於效能的考量， **check on change** 評估模式並未支援所有原則與任意物件集搭配使用。 如需詳細資訊，請參閱 [https://blogs.msdn.com/b/sqlpbm/archive/2009/04/13/policy-evaluation-modes.aspx](https://blogs.msdn.com/b/sqlpbm/archive/2009/04/13/policy-evaluation-modes.aspx)  
  
## <a name="three-policy-based-management-components"></a>三個原則式管理元件  
 原則式管理有三個元件：  
  
-   原則管理。 原則管理員會建立原則。  
  
-   明確管理。 管理員會選取一或多個 Managed 目標並且明確檢查這些目標是否符合特定原則，或明確讓這些目標符合原則。  
  
-   評估模式。 有四種評估模式，其中三種模式可以自動化：  
  
    -   **視需要**。 這種模式會在使用者直接指定時評估原則。  
  
    -   **變更時: 避免**。 這種自動模式會使用 DDL 觸發程序來防止原則違規。  
  
        > **重要！** 如果停用了巢狀觸發程序伺服器組態選項，[變更時: 避免]  將無法正確運作。 以原則為基礎的管理會依賴 DDL 觸發程序來偵測及回復不符合使用此評估模式之原則的 DDL 作業。 移除以原則為基礎的管理 DDL 觸發程序或停用巢狀觸發程序時，將會造成這個評估模式失敗或以非預期的方式執行。  
  
    -   **變更時: 僅限記錄**。 這種自動模式會在發生相關變更時使用事件通知來評估原則。  
  
    -   **按排程時間**。 這種自動模式會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業來定期評估原則。  
  
     未啟用自動原則時，原則式管理將不會影響系統效能。  
  
## <a name="terms"></a>詞彙  
 **原則式管理 Managed 目標**：以原則式管理所管理的實體，例如 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的執行個體、資料庫、資料表或索引。 伺服器執行個體中的所有目標都會構成目標階層。 目標集是指將一組目標篩選套用至目標階層所產生的目標集，例如 HumanResources 結構描述所擁有之資料庫中的所有資料表。  
  
 **原則式管理 Facet：** 為特定 Managed 目標類型建立行為或特性建立模型的一組邏輯屬性。 屬性的數目和特性會建立在 Facet 中，而且只能由 Facet 的建立者加入或移除。 一個目標類型可以實作一或多個管理 Facet，而一個管理 Facet 可以由一或多個目標類型實作。 Facet 的某些屬性只能套用至特定版本。  
  
 **以原則為基礎的管理條件**  
 一種布林運算式，可指定以原則為基礎之管理 Managed 目標所允許的一組狀態 (與管理 Facet 有關)。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在評估條件時嘗試觀察定序。 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 定序不完全符合 Windows 定序時，請測試您的條件，以決定演算法如何解決衝突。  
  
 **以原則為基礎的管理原則**  
 以原則為基礎的管理條件和預期的行為，例如評估模式、目標篩選和排程。 一個原則只能包含一個條件。 您可以啟用或停用原則。 原則會儲存在 msdb 資料庫中。  
  
 **以原則為基礎的管理原則類別目錄**  
 協助管理原則的使用者定義類別目錄。 使用者可以將原則分類至不同的原則類別目錄中。 一個原則只能屬於一個原則類別目錄。 原則類別目錄會套用至資料庫和伺服器。 下列條件會在資料庫層級套用：  
  
-   資料庫擁有者可以讓資料庫訂閱一組原則類別目錄。  
  
-   只有來自其訂閱類別目錄的原則可以管理資料庫。  
  
-   所有資料庫都會隱含訂閱預設的原則類別目錄。  
  
 原則類別目錄可以在伺服器層級上套用到所有資料庫。  
  
 **有效原則**  
 目標的有效原則就是管理此目標的這些原則。 只有在滿足下列所有條件時，原則對於目標而言才有效：  
  
-   此原則已啟用。  
  
-   目標屬於此原則的目標集。  
  
-   目標或其中一個目標上階，訂閱了包含此原則的原則群組。  
  
## <a name="links-to-specific-tasks"></a>特定工作的連結 

 - [儲存原則式管理原則。](policy-based-management-storage.md)|  
 - [設定警示以便向原則管理員通知原則失敗](../../relational-databases/policy-based-management/configure-alerts-to-notify-policy-administrators-of-policy-failures.md)  
 - [建立新的原則式管理條件](../../relational-databases/policy-based-management/create-a-new-policy-based-management-condition.md) 
 - [刪除原則式管理條件](../../relational-databases/policy-based-management/delete-a-policy-based-management-condition.md)
 - [檢視或修改原則式管理條件的屬性](../../relational-databases/policy-based-management/view-or-modify-the-properties-of-a-policy-based-management-condition.md)|  
 - [匯出原則式管理原則](../../relational-databases/policy-based-management/export-a-policy-based-management-policy.md)
 - [匯入原則式管理原則](../../relational-databases/policy-based-management/import-a-policy-based-management-policy.md)|  
 - [根據物件評估原則式管理原則](../../relational-databases/policy-based-management/evaluate-a-policy-based-management-policy-from-an-object.md)
 - [使用原則式管理 Facet](../../relational-databases/policy-based-management/working-with-policy-based-management-facets.md)|  
 - [使用原則式管理來監視和強制最佳做法](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)


## <a name="see-also"></a>另請參閱  
 
 - [教學課程：建立和套用預設關閉原則](lesson-1-create-and-apply-an-off-by-default-policy.md)
 - [教學課程：建立和套用命名標準原則](lesson-2-create-and-apply-a-naming-standards-policy.md)
 - [以原則為基礎的管理檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
 

 
  
  
