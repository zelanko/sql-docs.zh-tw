---
title: 專案設定 （同步處理） (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 2cd6bc01-b8e5-4312-83a4-eac66dc1d460
caps.latest.revision: 3
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: fcdcfc8d113bca42a9f042e8e6196d3de55b8e7e
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2018
ms.locfileid: "40395432"
---
# <a name="project-settings-synchronization-sybasetosql"></a>專案設定 (同步處理) (SybaseToSQL)
同步處理頁面**專案設定** 對話方塊中包含自訂 SSMA 到所載入的資料庫物件，例如資料表和預存程序，設定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。  
  
您可以存取兩個不同的同步處理頁面，其中包含相同的設定：  
  
-   如果您想要在指定為所有未來的 SSMA 專案，設定**工具**功能表上，選取**預設專案設定**，選取移轉的專案類型，則需要可以檢視或變更設定從**移轉目標版本**下拉式清單，然後選取**同步處理**左窗格的底部。  
  
-   若要指定目前的專案中，設定**工具**功能表上，選取**專案設定**，然後選取**同步處理**左窗格的底部。  
  
## <a name="options"></a>選項。  
**嘗試**  
指定載入物件時，應該要 SSMA 的嘗試次數[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 物件，不會載入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中目前嘗試將會重試，直到 SSMA 到達目前的同步處理程序中的嘗試次數上限。  
  
## <a name="synchronization-for-sql-server"></a>適用於 SQL Server 的同步處理  
**重新整理本機和遠端物件的變更上的本機物件**  
指定 SSMA 是否本機和遠端物件的變更，是否應該取代的本機物件中繼資料與遠端物件中繼資料。  
如果您選取**從資料庫重新整理**，SSMA 會將載入資料庫定義的中繼資料時即符合此條件。  
如果您選取**寫入資料庫**，SSMA 在符合條件時，會更新根據 SSMA 中繼資料內容，在資料庫中的物件。  
如果您選取**略過**，SSMA 將不會執行重新整理的任何動作。   
設定預設選項是**寫入資料庫。**  
  
**重新整理本機物件變更的本機物件**  
指定 SSMA 遠端物件變更時，是否應該取代本機物件中繼資料與遠端物件中繼資料。  
如果您選取**從資料庫重新整理**，SSMA 會將載入資料庫定義的中繼資料時即符合此條件。  
如果您選取**寫入資料庫**，SSMA 在符合條件時，會更新根據 SSMA 中繼資料內容，在資料庫中的物件。  
如果您選取**略過**，SSMA 將不會執行重新整理的任何動作。   
設定預設選項是**寫入資料庫**。  
  
**重新整理遠端物件的變更上的本機物件**  
指定 SSMA 遠端物件變更時，是否應該取代本機物件中繼資料與遠端物件中繼資料。  
如果您選取**從資料庫重新整理**，SSMA 會將載入資料庫定義的中繼資料時即符合此條件。  
如果您選取**寫入資料庫**，SSMA 在符合條件時，會更新根據 SSMA 中繼資料內容，在資料庫中的物件。  
如果您選取**略過**，SSMA 將不會執行重新整理的任何動作。   
設定預設選項是**從資料庫重新整理**。  
  
**重新整理時遺漏本機物件中繼資料**  
指定是否物件已存在目標資料庫，但不是在本機，SSMA 是否應該建立本機中繼資料。  
如果您選取**從資料庫重新整理**，SSMA 會選取從 [資料庫] 選項重新整理時即符合此條件。  
如果您選取**寫入資料庫**，SSMA 將物件從資料庫刪除時即符合此條件。  
如果您選取**略過**，SSMA 將不會執行重新整理的任何動作。   
設定預設選項是**從資料庫重新整理**。  
  
