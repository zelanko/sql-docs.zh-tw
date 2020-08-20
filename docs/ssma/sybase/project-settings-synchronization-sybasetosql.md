---
description: 專案設定 (同步處理) (SybaseToSQL)
title: " (同步處理)  (SybaseToSQL) 的專案設定 |Microsoft Docs"
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 2cd6bc01-b8e5-4312-83a4-eac66dc1d460
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 505df97bc8acbc0d3f55ef9c816ed4fb0c9bd569
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88497644"
---
# <a name="project-settings-synchronization-sybasetosql"></a>專案設定 (同步處理) (SybaseToSQL)
[ **專案設定** ] 對話方塊的 [同步處理] 頁面包含的設定，可自訂 SSMA 將資料庫物件（例如資料表和預存程式）載入至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL Azure 的方式。  
  
您可以存取兩個不同的同步處理頁面，其中包含相同的設定：  
  
-   如果您想要為所有未來的 SSMA 專案指定設定，請在 [ **工具** ] 功能表上選取 [ **預設專案設定**]，選取 [遷移專案類型]，需要從 [ **遷移目標版本** ] 下拉式清單中查看或變更設定，然後選取左窗格底部的 **[同步** 處理]。  
  
-   若要指定目前專案的設定，請在 [ **工具** ] 功能表上選取 [ **專案設定**]，然後選取左窗格底部的 **[同步** 處理]。  
  
## <a name="options"></a>選項。  
**嘗試**  
指定將物件載入至時，SSMA 應該進行的嘗試次數 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 未 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在目前嘗試中載入的物件將會再次嘗試，直到 SSMA 達到目前同步處理處理常式的最大嘗試次數為止。  
  
## <a name="synchronization-for-sql-server"></a>SQL Server 的同步處理  
**在本機和遠端物件變更時重新整理本機物件**  
指定當本機和遠端物件變更時，SSMA 是否應該將本機物件中繼資料取代為遠端物件中繼資料。  
如果您選取 [ **從資料庫**重新整理]，SSMA 會在符合條件時將資料庫定義載入中繼資料。  
如果您選取 [ **寫入資料庫**]，SSMA 會在符合條件時，根據 SSMA 中繼資料內容來更新資料庫中的物件。  
如果您選取 [ **略過**]，SSMA 將不會執行任何重新整理動作。   
預設選項組是 **寫入資料庫。**  
  
**在本機物件變更時重新整理本機物件**  
指定如果遠端物件變更，SSMA 是否應該以遠端物件中繼資料來取代本機物件中繼資料。  
如果您選取 [ **從資料庫**重新整理]，SSMA 會在符合條件時將資料庫定義載入中繼資料。  
如果您選取 [ **寫入資料庫**]，SSMA 會在符合條件時，根據 SSMA 中繼資料內容來更新資料庫中的物件。  
如果您選取 [ **略過**]，SSMA 將不會執行任何重新整理動作。   
預設選項組是 **寫入資料庫**。  
  
**重新整理遠端物件上的本機物件變更**  
指定如果遠端物件變更，SSMA 是否應該以遠端物件中繼資料來取代本機物件中繼資料。  
如果您選取 [ **從資料庫**重新整理]，SSMA 會在符合條件時將資料庫定義載入中繼資料。  
如果您選取 [ **寫入資料庫**]，SSMA 會在符合條件時，根據 SSMA 中繼資料內容來更新資料庫中的物件。  
如果您選取 [ **略過**]，SSMA 將不會執行任何重新整理動作。   
**從資料庫**重新整理預設選項組。  
  
**缺少區域物件中繼資料時重新整理**  
指定如果物件存在於目標資料庫中，但不在本機上，SSMA 是否應該建立本機中繼資料。  
如果您選取 [ **從資料庫**重新整理]，SSMA 會在符合條件時選取 [從資料庫重新整理] 選項。  
如果您選取 [ **寫入資料庫**]，則當符合條件時，SSMA 會從資料庫中刪除物件。  
如果您選取 [ **略過**]，SSMA 將不會執行任何重新整理動作。   
**從資料庫**重新整理預設選項組。  
  
