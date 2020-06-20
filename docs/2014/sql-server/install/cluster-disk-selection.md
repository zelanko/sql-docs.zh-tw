---
title: 叢集磁片選取 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- cluster disk selection
ms.assetid: 0d6b863d-5972-4a20-9990-64ee8016fea6
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 0f53d6d3f623254d2b17996be7fd5b8235dca223
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85037120"
---
# <a name="cluster-disk-selection"></a>叢集磁碟選取
  您可以使用 **安裝精靈的** [叢集磁碟選取] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 頁面來選取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集的共用叢集磁碟資源。 叢集磁碟就是即將放置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料的位置。  
  
 共用叢集磁片不是叢集安裝的必要條件 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 。 SMB 檔案伺服器是容錯移轉叢集安裝的支援儲存體 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] ，而且可以在完成安裝之前，使用 [**資料庫引擎-資料目錄**] 頁面來指定。  
  
> [!WARNING]  
>  如果您已經選取了要安裝 Analysis Services，就必須指定共用叢集磁碟。  
>   
>  如果您計畫在這個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體上啟用 FILESTREAM，就必須指定共用叢集磁碟。  
  
## <a name="options"></a>選項  
 **共用磁片**  
 從清單中選取單一磁碟。 叢集磁碟就是即將放置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料的位置。  
  
 您只能指定一個磁碟。 如果您選取包含叢集仲裁資源的群組，則會出現警告。 我們建議您不要安裝到叢集仲裁資源。  
  
 **可用共用磁碟**  
 顯示可用磁碟的清單、每個磁碟是否具有成為共用磁碟的資格，以及每個磁碟資源的描述。  
  
  
