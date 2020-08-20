---
description: 設定專案選項 (OracleToSQL)
title: 設定專案選項 (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Configuration Options and Modes
ms.assetid: a324d07d-cfdf-43bd-98a0-acf332c5a4db
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: 89460a8efb6278d8e4aaa4def6310d6dec687429
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88492348"
---
# <a name="setting-project-options-oracletosql"></a>設定專案選項 (OracleToSQL)
您可以針對每個 SSMA 專案設定專案層級選項。 這些選項會指定物件轉換、物件載入、使用者介面和資料移轉設定。 將物件轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或將資料移轉至之前，請確認設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 選項適用于專案。  
  
SSMA 可讓您設定所有專案的預設選項。 這些選項會套用至您所建立的任何新專案。 然後，您可以自訂每個專案的選項。  
  
## <a name="configuration-options-and-modes"></a>設定選項和模式  
SSMA 有五組專案設定：  
  
-   專案資訊  
  
-   一般 (轉換、遷移、載入物件)   
  
-   Synchronization  
  
-   GUI  
  
-   型別對應  
  
它也有四種設定這些設定的模式：  
  
-   預設  
  
-   開放式  
  
-   完整  
  
-   自訂  
  
大部分的使用者都建議使用預設模式。 開放式模式會保留更多目前的 Oracle 語法，而且更容易閱讀。 不過，保留目前的語法可能不正確。 如果 Oracle 語法必須轉換成相等的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 語法，則完整模式會執行最完整的轉換，但產生的程式碼可能更難以讀取。 在自訂模式中，您可以設定選項。  
  
如需有關設定的詳細資訊，以及如何在每個模式中套用設定的詳細資訊，請參閱下列主題：  
  
-   [專案設定 &#40;轉換&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md)  
  
-   [&#40;遷移&#41; &#40;OracleToSQL&#41;的專案設定 ](../../ssma/oracle/project-settings-migration-oracletosql.md)  
  
-   [&#40;同步處理的專案設定&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-synchronization-oracletosql.md)  
  
-   [專案設定 &#40;GUI&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-gui-oracletosql.md)  
  
-   [專案設定 &#40;類型對應&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-type-mapping-oracletosql.md)  
  
## <a name="setting-project-options"></a>設定專案選項  
在 SSMA 中，您可以設定所有專案的預設設定。 這些設定會儲存至 SSMA 設定檔，並套用至您建立的任何新專案。  
  
**若要設定預設專案選項**  
  
1.  按一下 [ **工具** ] 功能表上的 [ **預設專案設定**]。  
  
2.  在 [ **預設專案設定** ] 對話方塊中，使用下列其中一個程式：  
  
    -   從左窗格底部的 [ **遷移目標版本** ] 下拉式清單按一下 **[一般** ]，選取需要在其上查看或變更設定的 [遷移專案類型]，然後選取 [轉換] 或 [遷移]。  
  
    -   若要選取預先定義的模式，請在 [ **模式]** 下拉式清單方塊中，選取 [ **預設**]、[ **開放式**] 或 [ **完整**]。  
  
    -   若要指定自訂設定，請選取或輸入新的設定或值。  
  
3.  按一下 [確定] **** 來儲存設定。  
  
您也可以自訂目前專案的設定。 這些設定會儲存至目前的專案檔。  
  
**自訂目前專案的設定**  
  
1.  按一下 [ **工具** ] 功能表上的 [ **專案設定**]。  
  
2.  在 [ **專案設定** ] 對話方塊中，使用下列其中一個程式：  
  
    -   若要選取預先定義的模式，請在 [ **模式]** 下拉式清單方塊中，選取 [ **預設**]、[ **開放式**] 或 [ **完整**]。  
  
    -   若要指定自訂模式，請在 [ **模式]** 方塊中選取 [ **自訂**]，然後選取適當的專案設定。  
  
3.  按一下 [確定] **** 來儲存設定。  
  
## <a name="next-steps"></a>後續步驟  
遷移的下一個步驟取決於您的專案需求：  
  
-   若要自訂來源和目標資料類型的對應，請參閱將 [Oracle 和 SQL Server 資料類型對應 &#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md)。  
  
-   否則，您可以將 Oracle 資料庫物件定義轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件定義。 如需詳細資訊，請參閱將 [Oracle 架構轉換 &#40;OracleToSQL&#41;](../../ssma/oracle/converting-oracle-schemas-oracletosql.md)。  
  
## <a name="see-also"></a>另請參閱  
[將 Oracle 和 SQL Server 資料類型對應 &#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md)  
  
