---
title: 叢集磁碟選取 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- cluster disk selection
ms.assetid: 0d6b863d-5972-4a20-9990-64ee8016fea6
caps.latest.revision: 9
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: ce08658fe769a356e4cd24e29ed094692892e48f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36034506"
---
# <a name="cluster-disk-selection"></a>叢集磁碟選取
  您可以使用 **安裝精靈的** [叢集磁碟選取] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 頁面來選取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集的共用叢集磁碟資源。 叢集磁碟就是即將放置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料的位置。  
  
 共用的叢集磁碟，就不需要針對[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)]叢集安裝。 SMB 檔案伺服器是支援的存放裝置，如[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)]容錯移轉叢集安裝，而且可以指定使用**Database Engine-資料目錄**完成安裝之前的頁面。  
  
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
  
  