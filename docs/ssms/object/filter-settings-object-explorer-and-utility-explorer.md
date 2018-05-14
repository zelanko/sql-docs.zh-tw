---
title: 篩選設定 (物件總管與公用程式總管) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-objects
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.common.filtersettings.f1
- sql13.ag.job.filtersettings.f1
ms.assetid: 4aab04bc-e1ab-4d4b-ab74-b287fc805bc2
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fb8e11f7d9b63e321b547595b10381f693f08cd6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="filter-settings-object-explorer-and-utility-explorer"></a>篩選設定 (物件總管與公用程式總管)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
使用此對話方塊來指定篩選。 篩選可以讓您將 [物件總管] 與 [公用程式總管] 設定為僅顯示符合特定準則的項目。 例如，您可以使用篩選，僅顯示名稱中包含單字「Maintenance」的作業。 [篩選設定] 對話方塊的標頭包含伺服器的名稱，也可以包含資料庫的名稱。  
  
## <a name="uielement-list"></a>UIElement 清單  
**屬性**  
顯示要根據該屬性進行篩選的屬性。  
  
**[運算子]**  
選取篩選將值套用到屬性的方式。 有下列的選項：  
  
-   **等於**  
  
    篩選會顯示屬性和值完全相符的項目。  
  
-   **包含**  
  
    篩選會顯示屬性包含值的項目。 屬性可以包含其他文字。  
  
-   **不包含**  
  
    篩選會顯示屬性不包含值的項目。  
  
-   **小於**  
  
    適用於日期，此篩選會顯示日期早於所提供之值的項目。  
  
-   **小於或等於**  
  
    適用於日期，此篩選會顯示日期包含或早於所提供之值的項目。  
  
-   **大於**  
  
    適用於日期，此篩選會顯示日期晚於所提供之值的項目。  
  
-   **大於或等於**  
  
    適用於日期，此篩選會顯示日期包含或晚於所提供之值的項目。  
  
-   **介於**  
  
    適用於日期，此篩選會顯示日期介於所提供之兩個日期之間的項目。 選取 [介於] 並按下 TAB 鍵新增另一個資料列，以輸入第二個日期。  
  
-   **不介於**  
  
    適用於日期，此篩選會顯示日期早於或晚於所提供之兩個日期的項目。 選取 [不介於] 並按下 TAB 鍵跳離 [運算子] 資料行，即可新增另一個資料列，以輸入第二個日期。  
  
**ReplTest1**  
輸入要和屬性比較的值。 針對日期，按一下向下鍵以顯示用來選取日期的日曆。  
  
**清除篩選**  
移除所有目前的篩選設定。  
  
## <a name="see-also"></a>另請參閱  
[使用 SQL Server Management Studio](../../ssms/use-sql-server-management-studio.md)  
[SQL Server 公用程式概觀](http://msdn.microsoft.com/en-us/6e6cbd25-6b1c-4e21-9ade-4584e243fd8f)  
  
