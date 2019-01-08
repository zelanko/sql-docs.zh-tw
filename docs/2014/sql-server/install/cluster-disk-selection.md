---
title: 叢集磁碟選取項目 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- cluster disk selection
ms.assetid: 0d6b863d-5972-4a20-9990-64ee8016fea6
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ea021ed6e3613d4a39641c582e0b091ebfe1a6f1
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52519656"
---
# <a name="cluster-disk-selection"></a>叢集磁碟選取
  您可以使用 **安裝精靈的** [叢集磁碟選取] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 頁面來選取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集的共用叢集磁碟資源。 叢集磁碟就是即將放置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料的位置。  
  
 共用的叢集磁碟不需要[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)]叢集安裝。 SMB 檔案伺服器是針對支援的儲存體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)]容錯移轉叢集安裝，而且可以指定使用**Database Engine-資料目錄**完成安裝之前的頁面。  
  
> [!WARNING]  
>  如果您已經選取了要安裝 Analysis Services，就必須指定共用叢集磁碟。  
>   
>  如果您計畫在這個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體上啟用 FILESTREAM，就必須指定共用叢集磁碟。  
  
## <a name="options"></a>選項。  
 **共用的磁碟**  
 從清單中選取單一磁碟。 叢集磁碟就是即將放置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料的位置。  
  
 您只能指定一個磁碟。 如果您選取包含叢集仲裁資源的群組，則會出現警告。 我們建議您不要安裝到叢集仲裁資源。  
  
 **可用共用的磁碟**  
 顯示可用磁碟的清單、每個磁碟是否具有成為共用磁碟的資格，以及每個磁碟資源的描述。  
  
  
