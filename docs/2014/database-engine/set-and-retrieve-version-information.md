---
title: 設定和擷取版本資訊 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- historical information [SQL Server]
- source controls [SQL Server Management Studio], version information
- retrieving version information
- current file version information
- version control services [SQL Server], retrieving version information
- version control services [SQL Server], setting version information
- status information [SQL Server], source control files
- historical information [SQL Server], source control files
ms.assetid: c3f253c4-4e3d-48e8-8d90-bd6ee899faf7
caps.latest.revision: 22
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0dde0359b67d34e712b76e53a855efaafc29b5b0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37265226"
---
# <a name="set-and-retrieve-version-information"></a>設定及擷取版本資訊
  版本資訊包括原始檔控制檔案的記錄和目前狀態。 [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe 會維護每個原始檔控制檔案的完整歷程，供您追蹤一或多個檔案在時間中的進展。 您也可以利用這項資訊來擷取檔案任何版本的本機副本，或比較任意兩個檔案版本。  
  
 檔案的記錄包括：  
  
-   版本號碼，用來識別它在相同檔案各其他版本之間的順序。  
  
-   執行的動作。 追蹤的作業包括檔案的建立、簽入和刪除。  
  
-   涉及檔案的動作之執行者的使用者名稱。  
  
-   作業的執行日期和時間。  
  
 另外，Visual SourceSafe 也會維護目前載入的方案之目前的狀態資訊。 這項資訊提供檔案目前狀態的快照，其中包括：  
  
-   簽出檔案之使用者的識別。  
  
-   所選檔案最新的版本號碼。  
  
-   版本的建立日期。  
  
-   版本的相關使用者註解。  
  
-   共用檔案之專案的路徑。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [檢視檔案記錄](../../2014/database-engine/view-file-history.md)  
  
-   [檢視專案記錄](../../2014/database-engine/view-project-history.md)  
  
-   [檢視檔案狀態](../../2014/database-engine/view-file-status.md)  
  
-   [擷取檔案](../../2014/database-engine/retrieve-files.md)  
  
-   [將版本指定為最新版](../../2014/database-engine/specify-a-version-as-the-latest-version.md)  
  
-   [比較檔案](../../2014/database-engine/compare-files.md)  
  
-   [共用檔案](../../2014/database-engine/share-files.md)  
  
-   [建立記錄和狀態報表](../../2014/database-engine/create-history-and-status-reports.md)  
  
## <a name="see-also"></a>另請參閱  
 [原始檔控制基本概念](../../2014/database-engine/source-control-basics.md)  
  
  
