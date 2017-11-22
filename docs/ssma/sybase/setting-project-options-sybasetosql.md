---
title: "設定專案選項 (SybaseToSQL) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords: Project Options Setting
ms.assetid: 97b70fc8-1f68-4f15-8e22-db5b784ea4ec
caps.latest.revision: "9"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d53fbd93f9b7d2a111185a04facaf4d39e7f0d98
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="setting-project-options-sybasetosql"></a>設定專案選項 (SybaseToSQL)
每個 SSMA 專案，您可以設定專案層級選項。 這些選項會指定物件轉換、 載入物件、 SQL azure、 使用者介面和資料移轉設定。 轉換物件之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 移轉資料或[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，請確認您的組態選項都適用於專案。  
  
SSMA 會讓您設定的所有專案的預設選項。 這些選項會套用至任何您建立新的專案。 您可以自訂每個專案的選項。  
  
## <a name="configuration-options-and-modes"></a>設定選項和模式  
SSMA 會有五種專案設定：  
  
1.  專案資訊  
  
2.  一般 （轉換、 移轉和收集資料）  
  
3.  Synchronization  
  
4.  GUI  
  
5.  型別對應  
  
它也會有四種模式來設定這些設定：  
  
1.  預設值  
  
2.  開放式  
  
3.  完整  
  
4.  Custom  
  
對大多數使用者建議的預設模式。 開放式模式仍可繼續多個目前的 Sybase Adaptive Server Enterprise (ASE) 語法中，而且更方便閱讀。 不過，保留目前的語法可能不正確。 如果 ASE 語法必須轉換為對等項目[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 的語法，完整模式執行完整的轉換，但產生的程式碼可能會更難閱讀。 在 [自訂] 模式中，您可以設定選項。  
  
這份文件的使用者介面參考一節中說明的設定。 如需詳細的設定，以及如何將設定套用在每個模式的詳細資訊，請參閱下列主題：  
  
-   [專案設定 &#40;轉換 &#41;&#40;SybaseToSQL &#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md)  
  
-   [專案設定 &#40;移轉 &#41;&#40;SybaseToSQL &#41;](../../ssma/sybase/project-settings-migration-sybasetosql.md)  
  
-   [專案設定 &#40;同步處理 &#41;&#40;SybaseToSQL &#41;](../../ssma/sybase/project-settings-synchronization-sybasetosql.md)  
  
-   [專案設定 &#40;GUI &#41;&#40;SybaseToSQL &#41;](../../ssma/sybase/project-settings-gui-sybasetosql.md)  
  
-   [專案設定 &#40;型別對應 &#41;&#40;SybaseToSQL &#41;](../../ssma/sybase/project-settings-type-mapping-sybasetosql.md)  
  
-   [專案設定 &#40;Azure SQL DB &#41;&#40;SybaseToSQL &#41;](../../ssma/sybase/project-settings-azure-sql-db-sybasetosql.md)  
  
## <a name="setting-project-options"></a>設定專案選項  
SSMA，在您可以設定所有專案的預設設定。 這些設定會儲存 SSMA 組態檔，並套用至您建立任何新的專案。  
  
**若要設定預設專案選項**  
  
1.  在**工具**功能表上，選取**預設專案設定**。  
  
2.  在**預設專案設定**對話方塊，請使用下列程序的其中一個：  
  
    -   選取移轉專案類型，不需要檢視或變更設定**移轉的目標版本**卸除向下按一下 一般 左窗格底部，然後選取 轉換或移轉或 SQL Azure。  
  
    -   若要選取預先定義的模式中，在**模式**下拉式清單方塊中，選取**預設**， **Optimistic**，或**完整**。  
  
    -   若要指定自訂設定，請直接選取或輸入新的設定或值。  
  
3.  按一下**確定**儲存設定。  
  
您也可以自訂設定目前的專案。 這些設定會儲存到目前的專案檔。  
  
**若要自訂 目前的專案設定**  
  
1.  在**工具**功能表上，選取**專案設定**。  
  
2.  在**專案設定**對話方塊，請使用下列程序的其中一個：  
  
    -   若要選取預先定義的模式中，在**模式**下拉式清單方塊中，選取**預設**， **Optimistic**，或**完整**。  
  
    -   若要指定自訂模式，在**模式**下拉式清單方塊中，選取**自訂**、 左窗格中選取一個選項，按一下 設定 或 值在右窗格中，然後選取或輸入新的設定或值。  
  
3.  按一下**確定**儲存設定。  
  
## <a name="next-steps"></a>後續步驟  
移轉的下一個步驟取決於您專案的需求：  
  
-   如果您想自訂的來源和目標資料類型對應，請參閱[對應 Sybase ASE 和 SQL Server 資料類型 &#40;SybaseToSQL &#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md).  
  
-   否則，您可以將轉換成 Sybase 資料庫物件定義[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 物件定義。 如需詳細資訊，請參閱[轉換 Sybase ASE 資料庫物件 &#40;SybaseToSQL &#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md).  
  
## <a name="see-also"></a>請參閱＜  
[Sybase ASE 將資料庫移轉至 SQL Server-Azure SQL DB &#40;SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
