---
title: "專案設定 （移轉） (AccessToSQL) |Microsoft 文件"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Migration settings
- Project Settings dialog box, Migration
ms.assetid: 4caebc9c-8680-4b99-a8fa-89c43161c95d
caps.latest.revision: 14
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 3faaf19a1c591628ef97c4fe33fa0a54d4b077d5
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="project-settings-migration-accesstosql"></a>專案設定 （移轉） (AccessToSQL)
移轉專案設定可讓您設定如何將資料移轉到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。  
  
[移轉] 窗格位於**專案設定**和**預設專案設定**對話方塊。  
  
-   使用**專案設定**對話方塊來設定目前專案的組態選項。 若要移轉設定中，存取在**工具**功能表上，選取**專案設定**，按一下 **一般**左的窗格中，然後再按一下底部**移轉**。  
  
-   使用**預設專案設定**對話方塊來設定所有專案的組態選項。 若要移轉設定中，存取在**工具**功能表上，選取**預設專案設定**，選取 專案類型中的**移轉的目標版本**您想要存取的設定，請按一下下拉式方塊**一般**左的窗格中，然後再按一下底部**移轉**。  
  
## <a name="options"></a>選項  
**檢查條件約束**  
指定將資料加入至資料表時，SSMA 是否應該檢查條件約束。  
  
-   **預設模式**: False  
  
-   **開放式模式**: True  
  
-   **完整模式**: False  
  
**引發觸發程序**  
指定 SSMA 是否應該引發插入觸發程序時，它將資料加入至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料表。  
  
-   **預設模式**: False  
  
-   **開放式模式**: True  
  
-   **完整模式**: False  
  
**保留識別**  
指定是否要 SSMA 保存存取識別值時，它將資料加入至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 如果此值為 False，[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]指派的識別值。  
  
-   **預設模式**: True  
  
-   **開放式模式**: True  
  
-   **完整模式**: False  
  
**保留 Null**  
指定是否要 SSMA 保存來源資料中的 null 值時，它將資料加入至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，不論在中指定的預設值[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
-   **預設模式**: True  
  
-   **開放式模式**: False  
  
-   **完整模式**: True  
  
**資料表鎖定**  
指定當它將資料加入資料表資料移轉期間，SSMA 是否鎖定資料表。 如果值為 False，SSMA 會使用資料列鎖定。  
  
-   **預設模式**: True  
  
-   **開放式模式**: True  
  
-   **完整模式**: True  
  
**取代不受支援的日期**  
指定是否 SSMA 應該更正存取日期早於最舊的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]datetime 日期 (01 1753 年 1 月)。  
  
-   若要保留目前的日期值，請選取**不執行任何動作**。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]不會接受之前 01 年 1 月 1753年的日期的日期時間資料行中。 如果您使用較舊的日期，您必須將日期時間值轉換為字元的值。  
  
-   若要將之前 01 年 1 月 1753年的日期轉換成 NULL，選取**取代 NULL**。  
  
-   若要取代支援日期之前 01 年 1 月 1753年的日期，請選取**取代為最接近的支援日期**。 如果您選取此值，最接近預設會選取支援的日期作為 01 年 1 月 1753年。  
  
**批次大小**  
資料移轉期間使用的批次大小。 每個批次之後，會記錄交易。 根據預設，所有配置的批次大小為 10000。  
  
## <a name="see-also"></a>另請參閱  
[使用者介面 Reference(Access)](http://msdn.microsoft.com/en-us/af24c303-4a41-449b-9c86-d6558a97e839)  
  

