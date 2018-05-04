---
title: 全域設定 （對話方塊） (DB2ToSQL) |Microsoft 文件
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-db2
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 360e01bb-6347-4e2b-acda-0daa161ed33b
caps.latest.revision: 3
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: ae164bb796089542d8c4b3b6fe78b0f82a21cb3b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="global-settings-dialogs-db2tosql"></a>全域設定 （對話方塊） (DB2ToSQL)
使用的對話方塊頁面**通用設定**對話方塊來指定的預設使用者動作和 SSMA 的警告設定。  
  
若要存取對話方塊設定在**工具**功能表上，選取**通用設定**，按一下  **GUI**底部的左的窗格，然後選取**對話方塊**。  
  
## <a name="options"></a>選項  
**覆寫物件之前，即發出警告**  
SSMA 會將物件轉換成 SQL Server 中，當部分物件可能已存在於專案的 SQL Server 中繼資料。 這些物件可能已經轉換，或物件可能只需要在目標結構描述中相同名稱做為您要轉換的物件。  
  
您可以使用此選項來指定是否 SSMA 應該會提示您覆寫重複的物件定義：  
  
-   如果您選取**True**，SSMA 遇到重複的物件時，會顯示警告對話方塊。 在這個對話方塊中，您可以指定要覆寫個別物件或所有重複的物件，或略過個別物件或所有重複的物件。  
  
-   如果您選取**False**、**物件覆寫預設動作**選項會顯示您用來指定預設動作。  
  
**物件覆寫預設動作**  
如果您選取，會出現這個選項**False**如**覆寫物件之前，就發出警告**選項。  
  
使用此選項來指定預設的物件覆寫行為：  
  
-   如果您選取**True**，SSMA 會自動覆寫具有相同名稱且位於中要轉換的物件相同的目標結構描述中的 SQL Server 專案中繼資料物件。  
  
-   如果您選取**False**，SSMA 不會覆寫物件中繼資料轉換期間。  
  
