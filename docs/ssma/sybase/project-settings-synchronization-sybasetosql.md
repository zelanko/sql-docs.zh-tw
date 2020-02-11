---
title: 專案設定（同步處理）（SybaseToSQL） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 2cd6bc01-b8e5-4312-83a4-eac66dc1d460
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 663a4b1e49d1f81ce040254a2c8f39a1a1f84b38
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68028681"
---
# <a name="project-settings-synchronization-sybasetosql"></a>專案設定 (同步處理) (SybaseToSQL)
[**專案設定**] 對話方塊的 [同步處理] 頁面包含自訂 SSMA 如何將資料庫物件（例如資料表和預存程式） [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]載入或 SQL Azure 的設定。  
  
您可以存取兩個包含相同設定的不同同步處理頁面：  
  
-   如果您想要指定所有未來 SSMA 專案的設定，請在 [**工具**] 功能表上，選取 [**預設專案設定**]，然後從 [**遷移目標版本**] 下拉式選單選取 [需要查看或變更設定] 的 [遷移專案類型]，然後選取左窗格底部的 **[同步**處理]。  
  
-   若要指定目前專案的設定，請在 [**工具**] 功能表上，選取 [**專案設定**]，然後選取左窗格底部的 **[同步**處理]。  
  
## <a name="options"></a>選項。  
**機會**  
指定在將物件載入至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時，SSMA 應該進行的嘗試次數。 目前嘗試[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中未載入的物件將會再次嘗試，直到 SSMA 達到目前同步處理常式的最大嘗試次數為止。  
  
## <a name="synchronization-for-sql-server"></a>SQL Server 的同步處理  
**重新整理本機和遠端物件變更上的本機物件**  
指定當本機和遠端物件變更時，SSMA 是否應該將本機物件中繼資料取代為遠端物件中繼資料。  
如果您選取 [**從資料庫**重新整理]，SSMA 會在符合條件時，將資料庫定義載入中繼資料。  
如果您選取 [**寫入資料庫**]，SSMA 會根據符合條件時的 SSMA 中繼資料內容，更新資料庫中的物件。  
如果您選取 [**略過**]，SSMA 將不會執行任何重新整理動作。   
預設選項群組會**寫入資料庫。**  
  
**在本機物件變更時重新整理本機物件**  
指定如果遠端物件變更，SSMA 是否應該以遠端物件中繼資料來取代本機物件中繼資料。  
如果您選取 [**從資料庫**重新整理]，SSMA 會在符合條件時，將資料庫定義載入中繼資料。  
如果您選取 [**寫入資料庫**]，SSMA 會根據符合條件時的 SSMA 中繼資料內容，更新資料庫中的物件。  
如果您選取 [**略過**]，SSMA 將不會執行任何重新整理動作。   
預設選項群組會**寫入資料庫**。  
  
**重新整理遠端物件變更上的本機物件**  
指定如果遠端物件變更，SSMA 是否應該以遠端物件中繼資料來取代本機物件中繼資料。  
如果您選取 [**從資料庫**重新整理]，SSMA 會在符合條件時，將資料庫定義載入中繼資料。  
如果您選取 [**寫入資料庫**]，SSMA 會根據符合條件時的 SSMA 中繼資料內容，更新資料庫中的物件。  
如果您選取 [**略過**]，SSMA 將不會執行任何重新整理動作。   
預設選項組是 [**從資料庫**重新整理]。  
  
**在遺漏本機物件中繼資料時重新整理**  
指定如果目標資料庫（但不在本機）上有物件存在，SSMA 是否應該建立本機中繼資料。  
如果您選取 [**從資料庫**重新整理]，SSMA 會在符合條件時，從資料庫選取 [重新整理] 選項。  
如果您選取 [**寫入資料庫**]，當符合條件時，SSMA 將會從資料庫中刪除物件。  
如果您選取 [**略過**]，SSMA 將不會執行任何重新整理動作。   
預設選項組是 [**從資料庫**重新整理]。  
  
