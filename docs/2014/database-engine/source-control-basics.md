---
title: 原始檔控制基本概念 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- source controls [SQL Server Management Studio], providers
- source controls [SQL Server Management Studio]
- source controls [SQL Server Management Studio], about source controls
- source controls [SQL Server Management Studio], clients
ms.assetid: ca35b67a-104a-41fb-ac58-a61be06fe114
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bce3bd6862e612a8cefa35d1c981d608bf2c341c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62842982"
---
# <a name="source-control-basics"></a>原始檔控制基本概念
  「原始檔控制」是指利用一段中央伺服器軟體來儲存和追蹤檔案版本及控制檔案存取動作的系統。 典型的原始檔控制系統包括一個原始檔控制提供者及兩個或更多原始檔控制用戶端。  
  
## <a name="source-control-benefits"></a>原始檔控制的好處  
 將檔案放在原始檔控制之下，就能夠執行下列動作：  
  
-   管理在不同人員之間傳遞項目控制權的程序。 原始檔控制提供者支援共用和獨佔兩種檔案存取模式。 如果專案檔的存取是獨佔的，原始檔控制提供者每次只允許一位使用者簽出和修改檔案。 如果存取是共用的，便可以讓多位使用者簽出指令碼檔案，在各版本簽入時，原始檔控制提供者會提供用來合併它們的機制。  
  
-   保存原始檔控制項目的連續版本。 原始檔控制提供者會儲存用來區分原始檔控制項目各個版本的資料。 提供者會將版本之間的差異儲存起來，也會將版本的重要資訊儲存起來，其中包括它的建立時間、修改時間，以及修改者。 當許多人在處理相同的檔案時，他們必須使用相同的字碼頁，以便能夠精確地比較版本。 因此，您可以擷取原始檔控制項目的任何版本。 您也可以將任何版本指定為這個項目的最新版本。  
  
-   維護原始檔控制項目的詳細歷程和版本資訊。 原始檔控制會儲存項目的建立日期和時間、簽出或簽入的時間，以及執行動作的使用者。  
  
-   跨專案的協同運作。 檔案的共用使得多個專案有可能共用相同的原始檔控制項目。 共用項目的變更，會反映在共用這個項目的所有專案中。  
  
-   自動執行經常重複的原始檔控制作業。 原始檔控制提供者可以從命令提示字元之下，定義一個支援原始檔控制主要功能的介面。 您可以在批次檔中利用這個介面來自動執行您定期執行的原始檔控制工作。  
  
-   從意外刪除中復原。 您可以還原簽入原始檔控制中的最新檔案版本。  
  
-   節省原始檔控制用戶端和伺服器的磁碟空間。 部份原始檔控制提供者 (如 [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe) 支援儲存檔案的最新版本及各版本之間的差異，以節省伺服器的磁碟空間。 Visual SourceSafe 支援節省用戶端的磁碟空間。 您可以隱藏資料夾和檔案，使它們不會下載到您的本機磁碟中。  
  
 檔案的簽出、簽入及其他原始檔控制作業，實際上，都是由 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 之類的原始檔控制用戶端來完成的。 用戶端的設計就是為了與提供者互動，以便將提供者的功能提供給分散的使用者群組使用。 當使用原始檔控制用戶端時，使用者可以瀏覽提供者所儲存的檔案、加入和刪除檔案、簽入和簽出檔案，以及擷取本機檔案副本。  
  
> [!NOTE]  
>  這份文件集假設您的原始檔控制提供者是 [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe。 如果您使用其他原始檔控制提供者，這份文件集和您在執行的軟體可能會不同。 如果不同，請參閱您的原始檔控制提供者的文件集。  
  
## <a name="related-tasks"></a>相關工作  
  
|||  
|-|-|  
|**工作**|**主題**|  
|設定原始檔控制選項|[設定原始檔控制選項](../../2014/database-engine/set-source-control-options.md)|  
|變更原始檔控制連接|[變更原始檔控制連接](../../2014/database-engine/change-source-control-connections.md)|  
|從原始檔控制中排除檔案|[從原始檔控制中排除檔案](../../2014/database-engine/exclude-files-from-source-control.md)|  
  
  
