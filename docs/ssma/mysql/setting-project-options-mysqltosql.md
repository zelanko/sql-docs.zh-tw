---
title: 設定專案選項 (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Setting project options,configuration options
ms.assetid: 08820d88-e157-4d49-9401-38580dd7ec2d
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 346fcd2ea7f83abcb9a5c23a22cb0eded76acc0e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67944683"
---
# <a name="setting-project-options-mysqltosql"></a>設定專案選項 (MySQLToSQL)
針對每個 SSMA 專案中，您可以設定專案層級的選項。 這些選項會指定如何轉換物件、 資料的移轉方式，和來源資料類型如何對應至目標資料類型。  您將物件轉換為 SQL Server 或 SQL Azure，或將資料移轉至 SQL Server 或 SQL Azure 之前，確認適用於專案的組態選項。  
  
SSMA 會讓您設定的所有專案的預設選項。 這些選項會套用至任何您所建立的新專案。 然後，您可以自訂每個專案的選項。  
  
## <a name="configuration-options-and-modes"></a>設定選項和模式  
SSMA 會有五種專案設定：  
  
-   專案資訊  
  
-   一般 （轉換、 移轉及 SQL Azure）  
  
-   Synchronization  
  
-   GUI  
  
-   類型對應  
  
專案設定可以設定四種方式：  
  
-   預設  
  
-   開放式  
  
-   完整  
  
-   自訂  
  
預設模式被建議用於大部分的使用者。 開放式模式能夠保留更多目前的 MySQL 語法，而且容易讀取。 不過，保留目前的語法可能不正確。 如果 MySQL 語法必須轉換成 SQL Server 或 SQL Azure 的對等語法，完整模式會執行最完整的轉換。 產生的程式碼，不過，可能更難以閱讀。 在 [自訂] 模式中，您可以設定選項。  
  
如需有關設定和設定每個模式的套用方式的詳細資訊，請參閱下列主題：  
  
-   [專案設定&#40;轉換&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md)  
  
-   [專案設定&#40;移轉&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-migration-mysqltosql.md)  
  
-   [專案設定 (GUI) （SSMA 一般）](https://msdn.microsoft.com/cf06baf1-8714-48a3-95dc-781f6ca53693)  
  
-   [專案設定&#40;類型對應&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md)  
  
-   [專案設定&#40;同步處理&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-synchronization-mysqltosql.md)  
  
-   [專案設定&#40;Azure SQL DB&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-azure-sql-db-mysqltosql.md)  
  
## <a name="setting-project-options"></a>設定專案選項  
SSMA 中，您可以設定所有專案的預設的設定。 這些設定會儲存到 SSMA 組態檔，並套用到任何您所建立的新專案。  
  
**若要設定預設專案選項**  
  
1.  在 **工具**功能表上，按一下**預設專案設定**。  
  
2.  在 **預設專案設定**對話方塊，請使用下列程序的其中一個：  
  
    1.  選取，則需要檢視 / 變更設定的移轉專案類型**移轉目標版本**下拉式清單中，按一下**一般**在底部的左的窗格中，然後選取**資料轉換或 SQL Azure 移轉**選項。  
  
    2.  若要選取預先定義的模式，請選取**預設**， **Optimistic**，或**完整**從**模式**下拉式清單方塊。  
  
    3.  若要指定自訂的設定，請選取或輸入新的設定或值。  
  
3.  按一下 **確定**以儲存設定。  
  
您也可以自訂目前專案的設定。 取得目前的專案檔中儲存設定。  
  
**若要自訂目前專案的設定**  
  
1.  在 **工具**功能表上，按一下**ProjectSettings**。  
  
2.  在  **ProjectSettings**對話方塊，請使用下列程序的其中一個：  
  
    1.  若要選取預先定義的模式，請選取**預設**， **Optimistic**，或**完整**從**模式**下拉式清單方塊。  
  
    2.  若要指定自訂的模式，請選取**自訂**從**模式**下拉式清單方塊。 然後選取適當的專案設定。  
  
3.  按一下 **確定**以儲存設定。  
  
## <a name="next-step"></a>下一個步驟  
移轉的下一個步驟取決於您的專案需求：  
  
-   若要自訂的來源和目標資料類型對應，請參閱[對應 MySQL 和 SQL Server 資料類型&#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
-   否則，您可以轉換的 MySQL 資料庫物件定義 SQL Server 或 SQL Azure 物件定義。 如需詳細資訊，請參閱 <<c0> [ 轉換 MySQL 資料庫&#40;MySQLToSQL&#41;</c0>](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>另請參閱  
[對應 MySQL 和 SQL Server 資料類型&#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
