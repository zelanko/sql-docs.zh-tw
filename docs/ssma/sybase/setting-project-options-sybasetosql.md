---
title: 設定專案選項 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Project Options Setting
ms.assetid: 97b70fc8-1f68-4f15-8e22-db5b784ea4ec
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 9048eb69fd10cafc97daa91b5cac8571a4240cd0
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2018
ms.locfileid: "40392714"
---
# <a name="setting-project-options-sybasetosql"></a>設定專案選項 (SybaseToSQL)
針對每個 SSMA 專案中，您可以設定專案層級選項。 這些選項會指定物件轉換、 載入物件、 SQL azure、 使用者介面和資料移轉設定。 轉換物件之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 或移轉資料至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，確認組態選項都適用於專案。  
  
SSMA 會讓您設定的所有專案的預設選項。 這些選項會套用至任何您所建立的新專案。 然後，您可以自訂每個專案的選項。  
  
## <a name="configuration-options-and-modes"></a>設定選項和模式  
SSMA 會有五種專案設定：  
  
1.  專案資訊  
  
2.  一般 （轉換、 移轉和收集資料）  
  
3.  Synchronization  
  
4.  GUI  
  
5.  類型對應  
  
它也會有四種模式來設定這些設定：  
  
1.  預設  
  
2.  開放式  
  
3.  完整  
  
4.  Custom  
  
預設模式被建議用於大部分的使用者。 開放式模式能夠保留更多目前的 Sybase Adaptive Server Enterprise (ASE) 語法中，而且容易讀取。 不過，保留目前的語法可能不正確。 如果 ASE 語法必須轉換為對等[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 的語法的完整模式不會執行完整的轉換，但產生的程式碼可能更難以閱讀。 在 [自訂] 模式中，您可以設定選項。  
  
在這份文件中的使用者介面參考 > 一節中說明的設定。 如需有關設定和設定每個模式的套用方式的詳細資訊，請參閱下列主題：  
  
-   [專案設定&#40;轉換&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md)  
  
-   [專案設定&#40;移轉&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-migration-sybasetosql.md)  
  
-   [專案設定&#40;同步處理&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-synchronization-sybasetosql.md)  
  
-   [專案設定&#40;GUI&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-gui-sybasetosql.md)  
  
-   [專案設定&#40;類型對應&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-type-mapping-sybasetosql.md)  
  
-   [專案設定&#40;Azure SQL DB &#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-azure-sql-db-sybasetosql.md)  
  
## <a name="setting-project-options"></a>設定專案選項  
SSMA 中，您可以設定所有專案的預設的設定。 這些設定會儲存到 SSMA 組態檔，並套用到任何您所建立的新專案。  
  
**若要設定預設專案選項**  
  
1.  在 **工具**功能表上，選取**預設專案設定**。  
  
2.  在 **預設專案設定**對話方塊，請使用下列程序的其中一個：  
  
    -   選取移轉的專案類型，則需要可以檢視或變更設定**移轉目標版本**卸除向下按一下 一般，在左窗格底部，然後選取 資料轉換或 SQL Azure 移轉。  
  
    -   若要選取預先定義的模式中，在**模式**下拉式清單方塊中，選取**預設**， **Optimistic**，或**完整**。  
  
    -   若要指定自訂設定，只需選取或輸入新的設定或值。  
  
3.  按一下 **確定**以儲存設定。  
  
您也可以自訂設定目前的專案。 這些設定會儲存到目前的專案檔。  
  
**若要自訂目前專案的設定**  
  
1.  在 **工具**功能表上，選取**專案設定**。  
  
2.  在 **專案設定**對話方塊，請使用下列程序的其中一個：  
  
    -   若要選取預先定義的模式中，在**模式**下拉式清單方塊中，選取**預設**， **Optimistic**，或**完整**。  
  
    -   若要指定自訂模式中，在**模式**下拉式清單方塊中，選取**自訂**、 的左窗格中選取一個選項、 按一下 設定 或 值在右窗格中，然後選取或輸入新的設定或值。  
  
3.  按一下 **確定**以儲存設定。  
  
## <a name="next-steps"></a>後續步驟  
移轉的下一個步驟取決於您的專案需求：  
  
-   如果您想自訂的來源和目標資料類型對應，請參閱[對應 Sybase ASE 和 SQL Server 資料類型&#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)。  
  
-   否則，您可以將轉換至 Sybase 資料庫物件定義[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 物件定義。 如需詳細資訊，請參閱 <<c0> [ 轉換 Sybase ASE 資料庫物件&#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)。</c0>  
  
## <a name="see-also"></a>另請參閱  
[將 Sybase ASE 資料庫移轉至 SQL Server-Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
