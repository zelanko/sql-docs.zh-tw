---
title: 設定專案選項 (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f325a606-97ac-48bc-b344-b55f5e086a48
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 16bf79c185a23399d48d141b5d773e2e0d41dc3f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63269991"
---
# <a name="setting-project-options-db2tosql"></a>設定專案選項 (DB2ToSQL)
針對每個 SSMA 專案中，您可以設定專案層級選項。 這些選項會指定物件轉換、 載入物件、 使用者介面和資料移轉設定。 轉換物件之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或移轉資料至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，確認組態選項都適用於專案。  
  
SSMA 會讓您設定的所有專案的預設選項。 這些選項會套用至任何您所建立的新專案。 然後，您可以自訂每個專案的選項。  
  
## <a name="configuration-options-and-modes"></a>設定選項和模式  
SSMA 會有五種專案設定：  
  
-   專案資訊  
  
-   一般 （轉換、 載入物件的移轉）  
  
-   Synchronization  
  
-   GUI  
  
-   類型對應  
  
它也會有四種模式來設定這些設定：  
  
-   預設  
  
-   開放式  
  
-   完整  
  
-   自訂  
  
預設模式被建議用於大部分的使用者。 開放式模式能夠保留更多目前的 DB2 語法，而且容易讀取。 不過，保留目前的語法可能不正確。 如果 DB2 語法必須轉換為對等[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]完整模式的語法不會執行最完整的轉換，但產生的程式碼可能會較難閱讀。 在 [自訂] 模式中，您可以設定選項。  
  
如需有關設定和設定每個模式的套用方式的詳細資訊，請參閱下列主題：  
  
-   [專案設定&#40;轉換&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-conversion-db2tosql.md)  
  
-   [專案設定&#40;移轉&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-migration-db2tosql.md)  
  
-   [專案設定&#40;同步處理&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-synchronization-db2tosql.md)  
  
-   [專案設定&#40;GUI&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-gui-db2tosql.md)  
  
-   [專案設定&#40;類型對應&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-type-mapping-db2tosql.md)  
  
## <a name="setting-project-options"></a>設定專案選項  
SSMA 中，您可以設定所有專案的預設的設定。 這些設定會儲存到 SSMA 組態檔，並套用到任何您所建立的新專案。  
  
**若要設定預設專案選項**  
  
1.  在 **工具**功能表上，按一下**預設專案設定**。  
  
2.  在 **預設專案設定**對話方塊，請使用下列程序的其中一個：  
  
    -   選取移轉的專案類型，則需要可以檢視或變更設定**移轉目標版本**下拉式清單按一下**一般**在底部的左的窗格中，然後選取轉換或移轉。  
  
    -   若要選取預先定義的模式中，在**模式**下拉式清單方塊中，選取**預設**， **Optimistic**，或**完整**。  
  
    -   若要指定自訂的設定，請選取或輸入新的設定或值。  
  
3.  按一下 **確定**以儲存設定。  
  
您也可以自訂設定目前的專案。 這些設定會儲存到目前的專案檔。  
  
**若要自訂目前專案的設定**  
  
1.  在 **工具**功能表上，按一下**專案設定**。  
  
2.  在 **專案設定**對話方塊，請使用下列程序的其中一個：  
  
    -   若要選取預先定義的模式中，在**模式**下拉式清單方塊中，選取**預設**， **Optimistic**，或**完整**。  
  
    -   若要指定自訂模式中，在**模式**方塊中，選取**自訂**，然後選取適當的專案設定。  
  
3.  按一下 **確定**以儲存設定。  
  
## <a name="next-steps"></a>後續步驟  
移轉的下一個步驟取決於您的專案需求：  
  
-   若要自訂的來源和目標資料類型對應，請參閱[對應 DB2 和 SQL Server 資料類型&#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md)。  
  
-   否則，您可以將轉換到 DB2 資料庫物件定義[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]物件定義。 如需詳細資訊，請參閱 <<c0> [ 轉換 DB2 結構描述&#40;DB2ToSQL&#41;](../../ssma/db2/converting-db2-schemas-db2tosql.md)。</c0>  
  
## <a name="see-also"></a>另請參閱  
[對應 DB2 和 SQL Server 資料類型&#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md)  
  
