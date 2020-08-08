---
title: 全域設定 (對話方塊)  (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 6df20fbb-e92d-475f-a94d-aaf70b06eb9b
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 60629e8fda61af000f633f8f7ede714e48517f7c
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87935457"
---
# <a name="global-settings-dialogs-mysqltosql"></a> (對話方塊的全域設定)  (MySQLToSQL) 
使用 [**通用設定**] 對話方塊的 [對話方塊] 頁面，即可指定 SSMA 的預設使用者動作和警告設定。  
  
若要存取 [**工具**] 功能表上的對話方塊設定，請選取 [**全域設定**]，按一下左窗格底部的 [ **GUI** ]，然後選取 [**對話方塊**]。  
  
## <a name="options"></a>選項。  
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
  
