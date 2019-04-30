---
title: 全域設定 （對話方塊） (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 360e01bb-6347-4e2b-acda-0daa161ed33b
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: c0ac65e0973ac9e862a73dd9c04a916156c8a314
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63298794"
---
# <a name="global-settings-dialogs-db2tosql"></a>全域設定 （對話方塊） (DB2ToSQL)
使用對話方塊頁面**全域設定**對話方塊來指定預設使用者動作和 SSMA 的警告設定。  
  
若要存取對話方塊設定在**工具**功能表上，選取**全域設定**，按一下  **GUI**在底部的左的窗格中，然後選取**對話方塊**.  
  
## <a name="options"></a>選項。  
**覆寫物件之前，即發出警告**  
SSMA 會將物件轉換成 SQL Server 中，當某些物件可能已存在於專案的 SQL Server 中繼資料。 這些物件可能已經轉換，或物件可能是因為有在目標結構描述中相同名稱做為您要轉換的物件。  
  
您可以使用此選項來指定是否 SSMA 應該會提示您用來覆寫重複的物件定義：  
  
-   如果您選取 **，則為 True**，SSMA 會顯示警告對話方塊中，當它遇到重複的物件。 在此對話方塊中，您可以指定要覆寫個別物件或所有重複的物件，或略過個別物件或所有重複的物件。  
  
-   如果您選取**假**，則**物件覆寫預設動作**選項隨即出現，您可以在此指定的預設動作。  
  
**物件覆寫預設動作**  
如果您選取，會出現此選項**False**如**覆寫物件之前的警告**選項。  
  
您可以使用此選項來指定預設的物件覆寫行為：  
  
-   如果您選取 **，則為 True**，SSMA 會自動覆寫具有相同名稱且位於中要轉換的物件相同的目標結構描述中的 SQL Server 專案中繼資料物件。  
  
-   如果您選取**False**，SSMA 不能覆寫物件中繼資料轉換期間。  
  
