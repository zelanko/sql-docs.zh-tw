---
title: 設定轉換和移轉選項 (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- conversion, setting options
- migration options
- modes
- options, conversion settings
- project settings
- schemas
ms.assetid: 0a7304df-2f35-4453-96ef-7ac83dea1167
caps.latest.revision: 20
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 21cbf6f3a5dac0b77669b940bf27be26198a4456
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/16/2018
ms.locfileid: "40395866"
---
# <a name="setting-conversion-and-migration-options-accesstosql"></a>設定轉換和移轉選項 (AccessToSQL)
針對每個 SSMA 專案中，您可以設定專案層級的選項。 這些選項會指定如何轉換物件、 資料的移轉方式，和來源資料類型如何對應至目標資料類型。 轉換物件之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 或移轉資料至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，確認組態選項都適用於專案。  
  
## <a name="configuration-options-and-modes"></a>設定選項和模式  
SSMA 具有四組組態設定和設定這些設定值的四種模式： 預設、 Optimistic、 Full 和自訂。 預設模式被建議用於大部分的使用者。 使用開放式模式來進行簡單的轉換。 如果您想要查看所有訊息，請使用完整模式。 在 [自訂] 模式中，您可以設定選項。  
  
這份文件 」 使用者介面參考 > 一節中說明的設定。 如需有關設定和設定每個模式的套用方式的詳細資訊，請參閱下列主題：  
  
-   [專案設定 (轉換)](http://msdn.microsoft.com/bcebc635-c638-4ddb-924c-b9ccfef86388)  
  
-   [專案設定 (移轉)](http://msdn.microsoft.com/4caebc9c-8680-4b99-a8fa-89c43161c95d)  
  
-   [專案設定 (GUI)](http://msdn.microsoft.com/cf06baf1-8714-48a3-95dc-781f6ca53693)  
  
-   [專案設定 (類型對應)](http://msdn.microsoft.com/b87b9683-abed-4677-8c50-18bdba704655)  
  
-   [專案設定 (SQL Azure)](http://msdn.microsoft.com/bbb8a204-d0e4-4f0b-9709-271feb1f136e)  
  
## <a name="setting-project-options"></a>設定專案選項  
SSMA 中，您可以設定所有專案的預設的設定。 這些設定會儲存到 SSMA 組態檔，並套用到任何您所建立的新專案。  
  
**若要設定預設專案選項**  
  
1.  在 **工具**功能表上，選取**預設專案設定**。  
  
2.  在 [**預設專案設定**] 對話方塊中，執行下列其中之一：  
  
    -   選取，則需要檢視 / 變更設定的移轉專案類型**移轉目標版本**下拉式清單中，按一下**一般**在底部的左的窗格中，然後選取**資料轉換或 SQL Azure 移轉**。  
  
        > [!NOTE]  
        > SQL Azure 選項位於**一般**索引標籤上，只有建立的專案類型是 SQL Azure。  
  
    -   若要選取預先定義的模式，請選取**預設**， **Optimistic**，或**完整**中**模式**下拉式清單方塊。  
  
    -   若要指定自訂的模式，請選取**自訂**中**模式**，左窗格中選取一個選項、 按一下 設定 或 在右窗格中的值，然後選取或輸入新的設定或值。  
  
3.  按一下 **確定**以儲存設定。  
  
您也可以自訂設定目前的專案。 這些設定會儲存到目前的專案檔。  
  
**若要自訂目前專案的設定**  
  
1.  在 **工具**功能表上，選取**專案設定**。  
  
2.  在 [**專案設定**] 對話方塊中，執行下列其中之一：  
  
    -   若要選取預先定義的模式，請選取**預設**， **Optimistic**，或**完整**中**模式**下拉式清單方塊。  
  
    -   若要指定自訂的模式，請選取**自訂**中**模式**，左窗格中選取一個選項、 按一下 設定 或 在右窗格中的值，然後選取或輸入新的設定或值。  
  
3.  按一下 **確定**以儲存設定。  
  
## <a name="next-steps"></a>後續步驟  
移轉的下一個步驟取決於您的專案需求：  
  
-   若要自訂的來源和目標資料類型對應，請參閱[對應來源和目標資料類型](mapping-source-and-target-data-types-accesstosql.md)  
  
-   若要自訂的對應來源和目標資料庫，請參閱[對應來源和目標資料庫](mapping-source-and-target-databases-accesstosql.md)  
  
-   否則，您可以將轉換到存取資料庫物件定義[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 物件定義。 如需詳細資訊，請參閱[轉換 Access 資料庫物件](converting-access-database-objects-accesstosql.md)  
  
## <a name="see-also"></a>另請參閱  
[將 Access 資料庫移轉至 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
