---
description: " (對話方塊的全域設定)  (MySQLToSQL) "
title: " (對話方塊的全域設定)  (MySQLToSQL) |Microsoft Docs"
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 6df20fbb-e92d-475f-a94d-aaf70b06eb9b
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: e902927b90ff868e8766b3eb1fe9839938dd8ece
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88463413"
---
# <a name="global-settings-dialogs-mysqltosql"></a> (對話方塊的全域設定)  (MySQLToSQL) 
使用 [ **通用設定** ] 對話方塊的 [對話方塊] 頁面，即可指定 SSMA 的預設使用者動作和警告設定。  
  
若要存取 [ **工具** ] 功能表上的對話方塊設定，請選取 [ **全域設定**]，按一下左窗格底部的 [ **GUI** ]，然後選取 [ **對話方塊**]。  
  
## <a name="options"></a>選項。  
**覆寫物件之前警告**  
當 SSMA 將物件轉換為 SQL Server 時，某些物件可能已經存在於專案的 SQL Server 中繼資料中。 這些物件可能已經轉換，或物件在目標架構內的名稱可能會與您要轉換的物件相同。  
  
您可以使用此選項來指定 SSMA 是否應該提示您覆寫重複的物件定義：  
  
-   如果您選取 [ **True**]，則 SSMA 會在遇到重複的物件時顯示警告對話方塊。 在這個對話方塊中，您可以指定覆寫個別物件或所有重複的物件，或略過個別物件或所有重複的物件。  
  
-   如果您選取 [ **False**]，則會出現 [ **物件覆寫預設動作** ] 選項，讓您指定預設動作。  
  
**物件覆寫預設動作**  
如果您針對 [**覆寫物件之前警告**] 選項選取 [ **False** ]，則會出現此選項。  
  
使用這個選項來指定預設物件覆寫行為：  
  
-   如果您選取 [ **True**]，SSMA 會自動覆寫 SQL Server 專案中繼資料中的物件，該中繼資料具有相同的名稱，且與要轉換的物件位於相同的目標架構中。  
  
-   如果您選取 [ **False**]，SSMA 就不會在轉換期間覆寫物件中繼資料。  
  
