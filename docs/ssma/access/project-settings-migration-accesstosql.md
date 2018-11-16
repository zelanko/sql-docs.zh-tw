---
title: 專案設定 （移轉） (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Migration settings
- Project Settings dialog box, Migration
ms.assetid: 4caebc9c-8680-4b99-a8fa-89c43161c95d
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 441366208d2bfd886794dd7e50dca7e0aef7b3ff
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51659337"
---
# <a name="project-settings-migration-accesstosql"></a>專案設定 （移轉） (AccessToSQL)
移轉專案設定可讓您設定如何將資料移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。  
  
[移轉] 窗格位於**專案設定**並**預設專案設定**對話方塊。  
  
-   使用**專案設定**對話方塊來設定目前專案的組態選項。 若要存取的移轉設定中，在**工具**功能表上，選取**專案設定**，按一下 **一般**在底部的左的窗格中，然後按一下  **移轉**。  
  
-   使用**預設專案設定**對話方塊來設定的所有專案的組態選項。 若要存取的移轉設定中，在**工具**功能表上，選取**預設專案設定**，選取 專案類型中的**移轉目標版本**下拉式方塊，其中您要存取的設定，請按一下**一般**左的窗格中，然後再按一下底部**移轉**。  
  
## <a name="options"></a>選項。  
**檢查條件約束**  
指定 SSMA 是否應該將資料加入資料表檢查條件約束。  
  
-   **預設模式**: False  
  
-   **開放式模式**: True  
  
-   **完整模式**: False  
  
**引發觸發程序**  
指定 SSMA 是否應該引發插入觸發程序時，它將資料加入至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表。  
  
-   **預設模式**: False  
  
-   **開放式模式**: True  
  
-   **完整模式**: False  
  
**保留識別**  
指定是否 SSMA 會保留存取身分識別值時，它將資料加入至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果此值為 False，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]指派身分識別值。  
  
-   **預設模式**: True  
  
-   **開放式模式**: True  
  
-   **完整模式**: False  
  
**保留 Null**  
指定是否 SSMA 會保留來源資料中的 null 值時，它將資料加入至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，而不論在中指定的預設值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
-   **預設模式**: True  
  
-   **開放式模式**: False  
  
-   **完整模式**: True  
  
**資料表鎖定**  
指定時它會將資料加入資料表資料移轉期間 SSMA 是否鎖定資料表。 如果值為 False，SSMA 會使用資料列鎖定。  
  
-   **預設模式**: True  
  
-   **開放式模式**: True  
  
-   **完整模式**: True  
  
**取代不支援的日期**  
指定是否 SSMA 應該更正早於最舊存取日期[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]datetime 的日期 (01 1753 年 1 月)。  
  
-   若要保留目前的日期值，請選取**不執行任何動作**。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不會接受之前 01 年 1 月 1753年的日期的日期時間資料行中。 如果您使用較舊的日期，您必須將日期時間值轉換為字元。  
  
-   若要將 NULL 轉換之前 01 年 1 月 1753年的日期，請選取**取代為 NULL**。  
  
-   若要支援的日期取代之前 01 年 1 月 1753年的日期，請選取**最近支援的日期取代**。 如果您選取此值，最接近的預設支援的日期會被選為 01 年 1 月 1753年中。  
  
**批次大小**  
在資料移轉期間使用的批次大小。 每個批次之後，會記錄交易。 根據預設，所有配置的批次大小為 10000。  
  
## <a name="see-also"></a>另請參閱  
[使用者介面 Reference(Access)](https://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
