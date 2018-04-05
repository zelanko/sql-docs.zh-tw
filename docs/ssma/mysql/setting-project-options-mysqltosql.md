---
title: 設定專案選項 (MySQLToSQL) |Microsoft 文件
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Setting project options,configuration options
ms.assetid: 08820d88-e157-4d49-9401-38580dd7ec2d
caps.latest.revision: 12
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3aaec0d6811369af2ab4b5c52591af95fd944b57
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="setting-project-options-mysqltosql"></a>設定專案選項 (MySQLToSQL)
每個 SSMA 專案，您可以設定專案層級的選項。 這些選項會指定物件的轉換方式、 如何移轉資料和來源資料類型如何對應至目標資料類型。  您將物件轉換成 SQL Server 或 SQL Azure，或將資料移轉至 SQL Server 或 SQL Azure 之前，請確認組態選項都適用於專案。  
  
SSMA 會讓您設定的所有專案的預設選項。 這些選項會套用至您建立任何新的專案。 您可以自訂每個專案的選項。  
  
## <a name="configuration-options-and-modes"></a>設定選項和模式  
SSMA 會有五種專案設定：  
  
-   專案資訊  
  
-   一般 （轉換、 移轉和 SQL Azure）  
  
-   Synchronization  
  
-   GUI  
  
-   型別對應  
  
專案設定可以設定四種方式：  
  
-   預設  
  
-   開放式  
  
-   完整  
  
-   Custom  
  
對大多數使用者建議的預設模式。 開放式模式仍可繼續多個目前的 MySQL 語法，而且更方便閱讀。 不過，保留目前的語法可能不正確。 MySQL 語法必須轉換成 SQL Server 或 SQL Azure 的對等語法，如果完整模式執行的最完整的轉換。 產生的程式碼，不過，可能更難閱讀。 在 [自訂] 模式中，您可以設定選項。  
  
如需詳細的設定，以及如何將設定套用在每個模式的詳細資訊，請參閱下列主題：  
  
-   [專案設定 &#40;轉換 &#41;&#40;MySQLToSQL &#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md)  
  
-   [專案設定 &#40;移轉 &#41;&#40;MySQLToSQL &#41;](../../ssma/mysql/project-settings-migration-mysqltosql.md)  
  
-   [專案設定 (GUI) （SSMA 一般）](http://msdn.microsoft.com/en-us/cf06baf1-8714-48a3-95dc-781f6ca53693)  
  
-   [專案設定 &#40;型別對應 &#41;&#40;MySQLToSQL &#41;](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md)  
  
-   [專案設定 &#40;同步處理 &#41;&#40;MySQLToSQL &#41;](../../ssma/mysql/project-settings-synchronization-mysqltosql.md)  
  
-   [專案設定 &#40;Azure SQL DB &#41;&#40;MySQLToSQL &#41;](../../ssma/mysql/project-settings-azure-sql-db-mysqltosql.md)  
  
## <a name="setting-project-options"></a>設定專案選項  
SSMA，在您可以設定所有專案的預設設定。 這些設定會儲存 SSMA 組態檔，並套用至您建立任何新的專案。  
  
**若要設定預設專案選項**  
  
1.  在**工具**功能表上，按一下 **預設專案設定**。  
  
2.  在**預設專案設定**對話方塊，請使用下列程序的其中一個：  
  
    1.  選取移轉專案類型設定為需要從變更 / 檢視**移轉的目標版本**下拉式清單中，按一下 **一般**底部的左的窗格，然後選取**轉換或移轉或 SQL Azure**選項。  
  
    2.  若要選取預先定義的模式，請選取**預設**， **Optimistic**，或**完整**從**模式**下拉式清單方塊。  
  
    3.  若要指定自訂設定，請選取或輸入新的設定或值。  
  
3.  按一下**確定**儲存設定。  
  
您也可以自訂目前專案的設定。 取得目前的專案檔儲存設定。  
  
**若要自訂 目前的專案設定**  
  
1.  在**工具**功能表上，按一下  **ProjectSettings**。  
  
2.  在**ProjectSettings**對話方塊，請使用下列程序的其中一個：  
  
    1.  若要選取預先定義的模式，請選取**預設**， **Optimistic**，或**完整**從**模式**下拉式清單方塊。  
  
    2.  若要指定自訂的模式，請選取**自訂**從**模式**下拉式清單方塊。 然後選取適當的專案設定。  
  
3.  按一下**確定**儲存設定。  
  
## <a name="next-step"></a>下一個步驟  
移轉的下一個步驟取決於您專案的需求：  
  
-   若要自訂的來源和目標資料類型對應，請參閱[對應 MySQL 及 SQL Server 資料類型 &#40;MySQLToSQL &#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
-   否則，您可以將 MySQL 資料庫物件定義轉換成 SQL Server 或 SQL Azure 物件定義。 如需詳細資訊，請參閱[轉換 MySQL 資料庫 &#40;MySQLToSQL &#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>請參閱  
[對應 MySQL 及 SQL Server 資料類型 &#40;MySQLToSQL &#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
