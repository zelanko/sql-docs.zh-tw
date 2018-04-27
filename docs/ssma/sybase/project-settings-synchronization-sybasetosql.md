---
title: 專案設定 （同步處理） (SybaseToSQL) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 2cd6bc01-b8e5-4312-83a4-eac66dc1d460
caps.latest.revision: 3
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 49783b54640b82295b54450ad7eb63ea044e0721
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="project-settings-synchronization-sybasetosql"></a>專案設定 （同步處理） (SybaseToSQL)
同步處理頁面**專案設定**對話方塊包含自訂如何 SSMA 載入資料庫物件，例如資料表和預存程序，設定[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。  
  
您可以存取兩個不同的同步處理頁面包含相同的設定：  
  
-   如果您想在指定為所有未來的 SSMA 專案，設定**工具**功能表上，選取**預設專案設定**，選取移轉專案類型，不需要檢視或變更設定**移轉的目標版本**下拉式清單，然後選取**同步處理**在左窗格的底部。  
  
-   若要指定目前的專案中，設定**工具**功能表上，選取**專案設定**，然後選取**同步處理**在左窗格底部。  
  
## <a name="options"></a>選項  
**嘗試**  
指定將物件載入時，應該進行 SSMA 的嘗試次數[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 未載入的物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]中目前的嘗試將會重試直到 SSMA 到達目前的同步處理程序中的嘗試次數上限。  
  
## <a name="synchronization-for-sql-server"></a>SQL Server 的同步處理  
**重新整理本機和遠端物件變更的本機物件**  
指定 SSMA 是否本機和遠端物件的變更，是否應該取代本機物件中繼資料與遠端物件的中繼資料。  
如果您選取**從資料庫重新整理**，SSMA 會將載入資料庫定義的中繼資料時即符合此條件。  
如果您選取**寫入資料庫**，SSMA 滿足條件時，會更新根據 SSMA 中繼資料內容，在資料庫中的物件。  
如果您選取**略過**，SSMA 將不會執行重新整理的任何動作。   
設定預設選項是**寫入資料庫。**  
  
**重新整理本機物件變更的本機物件**  
指定 SSMA 遠端物件變更時，是否應該的本機物件中繼資料取代遠端物件的中繼資料。  
如果您選取**從資料庫重新整理**，SSMA 會將載入資料庫定義的中繼資料時即符合此條件。  
如果您選取**寫入資料庫**，SSMA 滿足條件時，會更新根據 SSMA 中繼資料內容，在資料庫中的物件。  
如果您選取**略過**，SSMA 將不會執行重新整理的任何動作。   
設定預設選項是**寫入資料庫**。  
  
**重新整理本機物件的遠端物件的變更**  
指定 SSMA 遠端物件變更時，是否應該的本機物件中繼資料取代遠端物件的中繼資料。  
如果您選取**從資料庫重新整理**，SSMA 會將載入資料庫定義的中繼資料時即符合此條件。  
如果您選取**寫入資料庫**，SSMA 滿足條件時，會更新根據 SSMA 中繼資料內容，在資料庫中的物件。  
如果您選取**略過**，SSMA 將不會執行重新整理的任何動作。   
設定預設選項是**從資料庫重新整理**。  
  
**遺漏本機物件的中繼資料時，重新整理**  
指定是否物件存在於目標資料庫，但不是在本機，SSMA 是否應該建立本機中繼資料。  
如果您選取**從資料庫重新整理**，SSMA 重新整理會從選取資料庫 選項時即符合此條件。  
如果您選取**寫入資料庫**，SSMA 將物件從資料庫中刪除時即符合此條件。  
如果您選取**略過**，SSMA 將不會執行重新整理的任何動作。   
設定預設選項是**從資料庫重新整理**。  
  
