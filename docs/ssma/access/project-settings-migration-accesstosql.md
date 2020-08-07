---
title: " (遷移的專案設定)  (AccessToSQL) |Microsoft Docs"
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
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 973a957f3c2c758aaf83116d9cba1cc8f50a3adc
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87937708"
---
# <a name="project-settings-migration-accesstosql"></a> (遷移)  (AccessToSQL 的專案設定) 
[遷移專案] 設定可讓您設定資料移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure 的方式。  
  
[**專案設定**] 和 [**預設專案設定**] 對話方塊中會提供 [遷移] 窗格。  
  
-   使用 [**專案設定**] 對話方塊，即可設定目前專案的配置選項。 若要存取遷移設定，請在 [**工具**] 功能表上，選取 [**專案設定**]，按一下左窗格底部的 **[一般**]，然後按一下 [**遷移**]。  
  
-   使用 [**預設專案設定**] 對話方塊，即可設定所有專案的設定選項。 若要存取遷移設定，請在 [**工具**] 功能表上，選取 [**預設專案設定**]，在您想要存取設定的 [**遷移目標版本**] 下拉式方塊中選取專案類型，按一下左窗格底部的 **[一般**]，然後按一下 [**遷移**]。  
  
## <a name="options"></a>選項。  
**檢查條件約束**  
指定在將資料加入資料表時，SSMA 是否應該檢查條件約束。  
  
-   **預設模式**： False  
  
-   **開放式模式**： True  
  
-   **完整模式**： False  
  
**引發觸發程序**  
指定在將資料新增至資料表時，SSMA 是否應該引發插入觸發程式 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
-   **預設模式**： False  
  
-   **開放式模式**： True  
  
-   **完整模式**： False  
  
**保留識別**  
指定當 SSMA 將資料新增至時，是否保留存取識別值 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如果此值為 False，則 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 指派識別值。  
  
-   **預設模式**： True  
  
-   **開放式模式**： True  
  
-   **完整模式**： False  
  
**保留 Null**  
指定在將資料新增至時，SSMA 是否會在來源資料中保留 null 值 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，而不論中指定的預設值為何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
-   **預設模式**： True  
  
-   **開放式模式**： False  
  
-   **完整模式**： True  
  
**表鎖**  
指定 SSMA 是否會在資料移轉期間將資料加入資料表時，鎖定資料表。 如果值為 False，則 SSMA 會使用資料列鎖定。  
  
-   **預設模式**： True  
  
-   **開放式模式**： True  
  
-   **完整模式**： True  
  
**取代不支援的日期**  
指定 SSMA 是否應該更正早于日期 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時間 (01 年1月 1753) 之前的存取日期。  
  
-   若要保留目前的日期值，請選取 [**不執行任何動作**]。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]將不會在日期時間資料行中接受01年 1753 1 月1日之前的日期。 如果您使用較舊的日期，您必須將日期時間值轉換成字元值。  
  
-   若要將在1753年1月01之前的日期轉換成 Null，請選取 [**以 Null 取代**]  
  
-   若要以支援的日期取代1753年1月之前的日期，請選取 [**取代為最接近的支援日期**]。 如果您選取此值，預設會將最接近的支援日期選取為01年1月1753。  
  
**批次大小**  
資料移轉期間使用的批次大小。 每個批次後都會記錄一個交易。 根據預設，所有配置的批次大小為10000。  
  
## <a name="see-also"></a>另請參閱  
[ (存取) 的使用者介面參考](https://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
