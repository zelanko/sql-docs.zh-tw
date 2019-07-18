---
title: 變更原始檔控制連接 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [SQL Server Management Studio], source controls
- source controls [SQL Server Management Studio], connections
ms.assetid: 538e3beb-f99c-4095-bd65-6413e872d26e
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d57f5938cb888a955645f5a9e0b01eeacfc1142b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62812787"
---
# <a name="change-source-control-connections"></a>變更原始檔控制連接
  您第一次從原始檔控制中加入或開啟方案時，您的原始檔控制提供者會建立本機方案目錄的根資料夾及其對應的伺服器資料夾之間的關聯。  
  
 根資料夾 (也稱為統一的根) 在用戶端。 您可以在這個資料夾之下，找到方案或專案所參考的所有檔案。 若要找到方案、方案記錄及其狀態資訊的最新版本，請先找出這個伺服器資料夾，它位於原始檔控制伺服器中。 在 [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe 中，伺服器資料夾稱為專案。  
  
 在許多情況之下，您都必須從方案的伺服器資料夾中，將方案解除繫結或中斷連接。 例如，如果無法使用原始檔控制提供者所在的電腦，您便無法依照正常方式來連接到備份電腦，請將方案重新繫結到備份伺服器資料夾，並繼續工作。 另外，如果原始檔控制專案分叉，您可能需要將方案繫結到新專案版本所在的伺服器資料夾。  
  
 請利用原始檔控制提供者的使用者介面來變更方案所繫結的伺服器資料夾。 您可以從 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 環境中開啟原始檔控制使用者介面。  
  
#### <a name="to-open-the-source-control-user-interface-from-the-studio-environment"></a>從 Studio 環境中開啟原始檔控制使用者介面  
  
1.  在 **檔案**功能表上，指向**原始檔控制**，然後按一下**啟動 Microsoft Visual SourceSafe**。  
  
## <a name="see-also"></a>另請參閱  
 [原始檔控制基本概念](../../2014/database-engine/source-control-basics.md)   
 [設定原始檔控制選項](../../2014/database-engine/set-source-control-options.md)   
 [從原始檔控制中排除檔案](../../2014/database-engine/exclude-files-from-source-control.md)  
  
  
