---
description: " (遷移)  (AccessToSQL) 的專案設定"
title: " (遷移)  (AccessToSQL) 的專案設定 |Microsoft Docs"
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
ms.openlocfilehash: 94bd5cc9a8cb0db9079db981ec50a5fa6af7b20c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88480524"
---
# <a name="project-settings-migration-accesstosql"></a> (遷移)  (AccessToSQL) 的專案設定
[遷移專案設定] 可讓您設定資料移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure 的方式。  
  
[ **專案設定** ] 和 [ **預設專案設定** ] 對話方塊中會提供 [遷移] 窗格。  
  
-   使用 [ **專案設定** ] 對話方塊，即可設定目前專案的設定選項。 若要存取遷移設定，請在 [ **工具** ] 功能表上選取 [ **專案設定**]，按一下左窗格底部的 **[一般** ]，然後按一下 [ **遷移**]。  
  
-   使用 [ **預設專案設定** ] 對話方塊，即可設定所有專案的設定選項。 若要存取遷移設定，請在 [ **工具** ] 功能表上選取 [ **預設專案設定**]，在您要存取設定的 [ **遷移目標版本** ] 下拉式方塊中，選取您要存取設定的專案類型，按一下左窗格底部的 **[一般** ]，然後按一下 [ **遷移**]。  
  
## <a name="options"></a>選項。  
**檢查條件約束**  
指定 SSMA 是否應該在將資料加入至資料表時檢查條件約束。  
  
-   **預設模式**： False  
  
-   **開放式模式**： True  
  
-   **完整模式**： False  
  
**引發觸發程序**  
指定 SSMA 是否應該在將資料加入至資料表時引發插入觸發程式 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
-   **預設模式**： False  
  
-   **開放式模式**： True  
  
-   **完整模式**： False  
  
**保留識別**  
指定當 SSMA 將資料新增至時，是否保留存取識別值 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如果這個值為 False，則 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 指派識別值。  
  
-   **預設模式**： True  
  
-   **開放式模式**： True  
  
-   **完整模式**： False  
  
**保留 Null**  
指定當 SSMA 將資料加入至時，是否在來源資料中保留 null 值 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，而不論中指定的預設值為何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
-   **預設模式**： True  
  
-   **開放式模式**： False  
  
-   **完整模式**： True  
  
**表鎖**  
指定當 SSMA 在資料移轉期間將資料加入資料表時，是否鎖定資料表。 如果值為 False，則 SSMA 會使用資料列鎖定。  
  
-   **預設模式**： True  
  
-   **開放式模式**： True  
  
-   **完整模式**： True  
  
**取代不支援的日期**  
指定 SSMA 是否應該更正早于最早日期 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時間日期 (01 年1月 1753) 的存取日期。  
  
-   若要保留目前的日期值，請選取 [ **不執行任何動作**]。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在日期時間資料行中，將不會接受1753年1月1日之前的日期。 如果您使用較舊的日期，則必須將日期時間值轉換為字元值。  
  
-   若要將01年1月 1753 1 日之前的日期轉換為 Null，請選取 [ **取代為 null**]  
  
-   若要以支援的日期取代01年1月 1753 1 日之前的日期，請選取 [ **以最接近的支援日期取代**] 如果您選取此值，預設會將最接近的支援日期選取為01年1月1753。  
  
**批次大小**  
資料移轉期間所使用的批次大小。 每個批次之後會記錄一筆交易。 依預設，所有配置的批次大小為10000。  
  
## <a name="see-also"></a>另請參閱  
[消費者介面參考 (存取) ](https://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
