---
title: 全域設定（對話方塊）（AccessToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 6c2204f2-d49e-49ba-9c0f-f14cf07fa561
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 5b8ef85b9d0d997ed8aae05fc53aa685a2dcacfa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67986413"
---
# <a name="global-settings-dialogs-accesstosql"></a>全域設定（對話方塊）（AccessToSQL）
使用 [**通用設定**] 對話方塊的 [對話方塊] 頁面，即可指定 SSMA 的預設使用者動作和警告設定。  
  
若要存取 [**工具**] 功能表上的對話方塊設定，請選取 [**全域設定**]，按一下左窗格底部的 [ **GUI** ]，然後選取 [**對話方塊**]。  
  
## <a name="options"></a>選項。  
**啟動時顯示遷移嚮導**  
在 [存取的 SSMA] 中，您可以選擇在啟動 SSMA 應用程式時啟用或停用 [**遷移嚮導]** 。 根據預設，此選項為**True**。  
  
-   如果選項設定為 [ **True**]，則會在您開啟 [存取應用程式的 SSMA] 時，一開始顯示 [遷移嚮導] 對話方塊。  
  
-   如果選項設定為**False**，則不會顯示 [遷移嚮導]，而且您必須在必要時從 [檔案 **] 功能表手動**存取它。  
  
**在覆寫物件之前發出警告**  
當 SSMA 將物件轉換成 SQL Server 時，某些物件可能已經存在於專案的 SQL Server 中繼資料中。 這些物件可能已經轉換，或物件在目標架構中的名稱可能與您要轉換的物件相同。  
  
使用此選項可指定 SSMA 是否應該提示您覆寫重複的物件定義：  
  
-   如果您選取 [ **True**]，當遇到重複的物件時，SSMA 會顯示警告對話方塊。 在此對話方塊中，您可以指定覆寫個別物件或所有重複的物件，或略過個別物件或所有重複的物件。  
  
-   如果您選取 [ **False**]，則會出現 [**物件覆寫預設動作**] 選項，您可以在其中指定預設動作。  
  
**物件覆寫預設動作**  
如果您在 [**覆寫物件之前警告**] 選項中選取 [ **False** ]，就會出現此選項。  
  
使用此選項來指定預設物件覆寫行為：  
  
-   如果您選取 [ **True**]，SSMA 會自動覆寫 SQL Server 專案中繼資料中，名稱相同且與要轉換之物件位於相同目標架構中的物件。  
  
-   如果您選取 [ **False**]，SSMA 在轉換期間不會覆寫物件中繼資料。  
  
