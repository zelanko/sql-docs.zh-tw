---
title: " (MySQLToSQL) 設定專案選項 |Microsoft Docs"
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Setting project options,configuration options
ms.assetid: 08820d88-e157-4d49-9401-38580dd7ec2d
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: cf8ac834b014fe49a851d3887fb36e29f59e069e
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87935126"
---
# <a name="setting-project-options-mysqltosql"></a>設定專案選項 (MySQLToSQL)
針對每個 SSMA 專案，您可以設定專案層級選項。 這些選項會指定物件的轉換方式、遷移資料的方式，以及源資料類型如何對應至目標資料類型。  將物件轉換成 SQL Server 或 SQL Azure，或將資料移轉至 SQL Server 或 SQL Azure 之前，請確認設定選項適用于專案。  
  
SSMA 可讓您設定所有專案的預設選項。 這些選項會套用至您所建立的任何新專案。 接著，您可以自訂每個專案的選項。  
  
## <a name="configuration-options-and-modes"></a>設定選項和模式  
SSMA 有五組專案設定：  
  
-   專案資訊  
  
-   一般 (轉換、遷移和 SQL Azure)   
  
-   Synchronization  
  
-   GUI  
  
-   類型對應  
  
您可以透過四種方式來設定專案設定：  
  
-   預設值  
  
-   開放式  
  
-   完整  
  
-   自訂  
  
建議大多數使用者使用預設模式。 開放式模式會保留更多目前的 MySQL 語法，而且較容易閱讀。 不過，保留目前的語法可能會不正確。 如果 MySQL 語法必須轉換成對等的 SQL Server 或 SQL Azure 語法，則完整模式會執行最完整的轉換。 不過，產生的程式碼可能會更容易閱讀。 在 [自訂] 模式中，您可以設定選項。  
  
如需有關設定以及如何在每個模式中套用設定的詳細資訊，請參閱下列主題：  
  
-   [專案設定 &#40;轉換&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md)  
  
-   [&#40;遷移&#41; &#40;MySQLToSQL 的專案設定&#41;](../../ssma/mysql/project-settings-migration-mysqltosql.md)  
  
-   [ (GUI)  (SSMA 通用) 的專案設定](https://msdn.microsoft.com/cf06baf1-8714-48a3-95dc-781f6ca53693)  
  
-   [專案設定 &#40;類型對應&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md)  
  
-   [&#40;同步處理的專案設定&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-synchronization-mysqltosql.md)  
  
-   [專案設定 &#40;Azure SQL Database&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-azure-sql-db-mysqltosql.md)  
  
## <a name="setting-project-options"></a>設定專案選項  
在 SSMA 中，您可以設定所有專案的預設設定。 這些設定會儲存到 SSMA 設定檔，並套用至您所建立的任何新專案。  
  
**若要設定預設專案選項**  
  
1.  在 [**工具**] 功能表上，按一下 [**預設專案設定**]。  
  
2.  在 [**預設專案設定**] 對話方塊中，使用下列其中一個程式：  
  
    1.  從 [**遷移目標版本**] 下拉式選視窗選取 [需要查看/變更設定] 的 [遷移專案類型]，然後按一下左窗格底部的 **[一般**]，再選取 [**轉換] 或 [遷移] 或 [SQL Azure** ] 選項。  
  
    2.  若要選取預先定義的模式，請從 [**模式]** 下拉式方塊中選取 [**預設**]、[**開放式**] 或 [**完整**]。  
  
    3.  若要指定自訂設定，請選取或輸入新的設定或值。  
  
3.  按一下 [確定] **** 來儲存設定。  
  
您也可以自訂目前專案的設定。 這些設定會儲存至目前的專案檔。  
  
**若要自訂目前專案的設定**  
  
1.  在 [**工具**] 功能表上，按一下 [ **ProjectSettings**]。  
  
2.  在 [ **ProjectSettings** ] 對話方塊中，使用下列其中一個程式：  
  
    1.  若要選取預先定義的模式，請從 [**模式]** 下拉式方塊中選取 [**預設**]、[**開放式**] 或 [**完整**]。  
  
    2.  若要指定自訂模式，請從 [**模式]** 下拉式方塊中選取 [**自訂**]。 然後選取適當的專案設定。  
  
3.  按一下 [確定] **** 來儲存設定。  
  
## <a name="next-step"></a>後續步驟  
遷移的下一個步驟取決於您的專案需求：  
  
-   若要自訂來源和目標資料類型的對應，請參閱將[MySQL 和 SQL Server 資料類型對應 &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
-   否則，您可以將 MySQL 資料庫物件定義轉換成 SQL Server 或 SQL Azure 物件定義。 如需詳細資訊，請參閱將[MySQL 資料庫轉換 &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>另請參閱  
[將 MySQL 和 SQL Server 資料類型對應 &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
