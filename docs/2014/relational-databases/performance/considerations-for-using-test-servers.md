---
title: 使用測試伺服器的考量 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- overhead [Database Engine Tuning Advisor]
- tuning overhead [SQL Server]
- reducing production server tuning load
- Database Engine Tuning Advisor [SQL Server], test servers
- xp_msver
- test servers [Database Engine Tuning Advisor]
- production servers [SQL Server]
- offload tuning overhead [SQL Server]
ms.assetid: 94e6c3e5-1f09-4616-9da2-4e44d066d494
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c1ed99e6ee3ef6385e6041044e9b2cb829b1b3ce
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63151147"
---
# <a name="considerations-for-using-test-servers"></a>使用測試伺服器的考量
  使用測試伺服器微調實際伺服器上的資料庫，是 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 的重要優點。 您可利用這項功能，在不需將實際資料從實際伺服器複製到測試伺服器的情況下，將微調負擔卸載到測試伺服器上。  
  
> [!NOTE]  
>  [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 圖形化使用者介面 (GUI) 不支援測試伺服器微調功能。  
  
 若要順利使用這項功能，請檢閱下列章節列出的考量事項。  
  
## <a name="setting-up-the-test-serverproduction-server-environment"></a>設定測試伺服器/實際伺服器環境  
  
-   要使用測試伺服器對實際伺服器上的資料庫進行微調的使用者，必須同時位於兩部伺服器上，否則此案例將會失敗。  
  
-   必須啟用擴充預存程序 **xp_msver**，才能使用測試伺服器/實際伺服器案例。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 會使用此擴充預存程序來提取在微調測試伺服器時實際伺服器上可使用的處理器數量與記憶體數量。 若未啟用 **xp_msver** ， [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 即會採用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 執行所在電腦的硬體特性。 如果無法取得執行 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 所在電腦的硬體特性，將會假設 1 個處理器和 1024 MB 的記憶體。 安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，預設會開啟擴充預存程序。 如需詳細資訊，請參閱[介面區組態](../security/surface-area-configuration.md)和 [xp_msver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/xp-msver-transact-sql)。  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 預期測試伺服器和實際伺服器上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本必須相同。 如果有兩種不同的版本，將優先採用測試伺服器上的版本。 例如，如果測試伺服器執行的是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard，即使實際伺服器執行的是 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Enterprise， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Tuning Advisor 也不會在其建議中包含索引檢視表、資料分割和線上作業。  
  
## <a name="about-test-serverproduction-server-behavior"></a>關於測試伺服器/實際伺服器的行為  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 在做出建議時，會將實際伺服器與測試伺服器之間的硬體差異列入考量。 這些建議就像是在單獨對實際伺服器完成微調的情況下所做的建議。  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 在收集中繼資料及建立必要的微調統計資料時，可能會對實際伺服器造成一些負荷。  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 不會從實際伺服器將實際資料複製到測試伺服器。 它只會複製資料庫的中繼資料與必要的統計資料。  
  
-   所有工作階段資訊都會儲存在實際伺服器的 **msdb** 中。 如此可讓您充分利用可進行微調的所有測試伺服器，且所有工作階段的相關資訊都會存放在同一個位置 (實際伺服器) 上。  
  
## <a name="issues-related-to-the-shell-database"></a>Shell 資料庫的相關問題  
  
-   在微調完成後， [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 會移除它在微調處理過程中於測試伺服器上建立的任何中繼資料。 其中包括 Shell 資料庫。 若您要以相同的實際伺服器與測試伺服器執行一系列的微調工作階段，您可以保留此 Shell 資料庫以節省時間。 請在 XML 輸入檔中，指定 **RetainShellDB** 子元素以及 **TuningOptions** 父元素下的其他子元素。 利用這些選項，[!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 就會保留 Shell 資料庫。 如需詳細資訊，請參閱 [XML 輸入檔參考 &#40;Database Engine Tuning Advisor&#41;](database-engine-tuning-advisor.md)。  
  
-   在順利完成測試伺服器/實際伺服器微調工作階段之後，即使您尚未指定 **RetainShellDB** 子元素，Shell 資料庫可能還是會留在測試伺服器上。 這些不需要的 Shell 資料庫可能會干擾後續的微調工作階段，因此應該在執行其他測試伺服器/實際伺服器微調工作階段之前加以卸除。 此外，如果有未預期的微調工作階段存在，測試伺服器上的 Shell 資料庫及這些資料庫中的物件都可能留在測試伺服器上。 啟動新的測試伺服器/實際伺服器微調工作階段之前，您也應該刪除這些資料庫和物件。  
  
## <a name="issues-related-to-the-tuning-process"></a>微調程序的相關問題  
  
-   使用者必須檢查微調記錄中，是否有因實際伺服器與測試伺服器之間的差異所導致的微調錯誤，以及因為從實際伺服器複製中繼資料到測試伺服器所導致的錯誤。 例如，測試伺服器上可能沒有使用者登入存在。 若測試伺服器上沒有使用者登入存在，則工作負載中這些由該使用者登入所發出的事件，將無法進行微調。 請使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor GUI 來檢視微調記錄。 如需詳細資訊，請參閱 [檢視及處理 Database Engine Tuning Advisor 的輸出](view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md)  
  
-   如果因為在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 建立於測試伺服器中的 Shell 資料庫中有物件遺漏，而使 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 無法微調多項事件，使用者必須檢查微調記錄。 無法微調的事件都會列在記錄檔中。 若要順利微調測試伺服器上的資料庫，使用者必須在 Shell 資料庫中建立遺漏的物件，然後啟動新的微調工作階段。  
  
-   若測試伺服器上已有同名的資料庫存在，則 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 不會複製中繼資料，但會繼續依需要進行微調並收集統計資料。 若使用者已在測試伺服器上建立資料庫，並在叫用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 之前複製了適當的中繼資料，就適用於這種情況。  
  
-   若實際伺服器上資料庫的 DATE_CORRELATION_OPTIMIZATION 選項已開啟，在微調測試伺服器時，與此選項關聯的中繼資料與資料不會完全指令碼化。 在測試伺服器/實際伺服器案例中執行微調時，可能會有下列問題：  
  
    -   對於使用 DATE_CORRELATION_OPTIMIZATION 選項的查詢，使用者可以在伺服器上擁有不同的查詢計畫。  
  
    -   [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 可能會建議卸除在建議指令碼中強制使用 DATE_CORRELATION_OPTIMIZATION 選項的索引檢視表。  
  
     因此，您可以忽略 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 對保存交互關聯統計資料之索引檢視所做的任何相關建議，因為 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 對它們的成本有所認知，對其利益則否。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 可能不會建議使用者選取特定的索引，例如 **datetime** 資料行中的叢集索引，而此索引在 DATE_CORRELATION_OPTIMIZATION 啟用的情況下應該會有益處。  
  
     若要判斷檢視是否以相互關聯統計資料為基礎，請選取 **sys.views** 目錄檢視的 [is_date_correlation_view](/sql/relational-databases/system-catalog-views/sys-views-transact-sql) 資料行。  
  
  
