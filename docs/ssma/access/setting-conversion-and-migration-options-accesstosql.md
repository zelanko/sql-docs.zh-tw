---
title: 設定轉換和遷移選項（AccessToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- conversion, setting options
- migration options
- modes
- options, conversion settings
- project settings
- schemas
ms.assetid: 0a7304df-2f35-4453-96ef-7ac83dea1167
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 3e89cfd6768aeedd970889cbaea46bb3e1ceae4f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68051504"
---
# <a name="setting-conversion-and-migration-options-accesstosql"></a>設定轉換和遷移選項（AccessToSQL）
針對每個 SSMA 專案，您可以設定專案層級選項。 這些選項會指定物件的轉換方式、遷移資料的方式，以及源資料類型如何對應至目標資料類型。 在您將物件轉換[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]為或 sql azure 或將資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]遷移至或 sql azure 之前，請先確認設定選項適用于專案。  
  
## <a name="configuration-options-and-modes"></a>設定選項和模式  
SSMA 有四組設定設定和四種模式來進行這些設定：預設值、開放式、完整和自訂。 建議大多數使用者使用預設模式。 使用開放式模式進行簡單轉換。 如果您想要查看所有訊息，請使用完整模式。 在自訂模式中，您可以設定選項。  
  
這些設定會在本檔的「使用者介面參考」一節中說明。 如需有關設定以及如何在每個模式中套用設定的詳細資訊，請參閱下列主題：  
  
-   [專案設定（轉換）](https://msdn.microsoft.com/bcebc635-c638-4ddb-924c-b9ccfef86388)  
  
-   [專案設定（遷移）](https://msdn.microsoft.com/4caebc9c-8680-4b99-a8fa-89c43161c95d)  
  
-   [專案設定 (GUI)](https://msdn.microsoft.com/cf06baf1-8714-48a3-95dc-781f6ca53693)  
  
-   [專案設定（類型對應）](https://msdn.microsoft.com/b87b9683-abed-4677-8c50-18bdba704655)  
  
-   [專案設定（SQL Azure）](https://msdn.microsoft.com/bbb8a204-d0e4-4f0b-9709-271feb1f136e)  
  
## <a name="setting-project-options"></a>設定專案選項  
在 SSMA 中，您可以設定所有專案的預設設定。 這些設定會儲存到 SSMA 設定檔，並套用至您所建立的任何新專案。  
  
**若要設定預設專案選項**  
  
1.  在 [**工具**] 功能表上，選取 [**預設專案設定**]。  
  
2.  在 [**預設專案設定**] 對話方塊中，執行下列其中一項動作：  
  
    -   從 [**遷移目標版本**] 下拉式選視窗選取 [需要查看/變更設定] 的 [遷移專案類型]，然後按一下左窗格底部的 **[一般**]，再選取 [**轉換] 或 [遷移] 或 [SQL Azure**]。  
  
        > [!NOTE]  
        > 只有在建立的專案類型是 SQL Azure 時，[**一般**] 索引標籤中才會提供 [sql azure] 選項。  
  
    -   若要選取預先定義的模式，請在 [**模式]** 下拉式方塊中選取 [**預設**]、[**開放式**] 或 [**完整**]。  
  
    -   若要指定自訂模式，請在 [**模式]** 方塊中選取 [**自訂**]，在左窗格中選取一個選項，按一下右窗格中的設定或值，然後選取或輸入新的設定或值。  
  
3.  按一下 [確定] **** 來儲存設定。  
  
您也可以自訂目前專案的設定。 這些設定會儲存至目前的專案檔。  
  
**若要自訂目前專案的設定**  
  
1.  在 [**工具**] 功能表上，選取 [**專案設定**]。  
  
2.  在 [**專案設定**] 對話方塊中，執行下列其中一項動作：  
  
    -   若要選取預先定義的模式，請在 [**模式]** 下拉式方塊中選取 [**預設**]、[**開放式**] 或 [**完整**]。  
  
    -   若要指定自訂模式，請在 [**模式]** 方塊中選取 [**自訂**]，在左窗格中選取一個選項，按一下右窗格中的設定或值，然後選取或輸入新的設定或值。  
  
3.  按一下 [確定] **** 來儲存設定。  
  
## <a name="next-steps"></a>後續步驟  
遷移的下一個步驟取決於您的專案需求：  
  
-   若要自訂來源和目標資料類型的對應，請參閱[對應來源和目標資料類型](mapping-source-and-target-data-types-accesstosql.md)  
  
-   若要自訂來源和目標資料庫的對應，請參閱[對應來源和目標資料庫](mapping-source-and-target-databases-accesstosql.md)  
  
-   否則，您可以將 Access 資料庫物件定義轉換成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 物件定義。 如需詳細資訊，請參閱[轉換 Access 資料庫物件](converting-access-database-objects-accesstosql.md)  
  
## <a name="see-also"></a>另請參閱  
[將 Access 資料庫移轉至 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
