---
title: "SQL Server 2012 SP2 版本資訊 | Microsoft Docs"
ms.prod: sql-server-2012
ms.technology: server-general
ms.custom: 
ms.date: 01/31/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 67cb8b3e-3d82-47f4-840d-0f12a3bff565
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 5e132652cc6464502785647f8a79dec5e25094c4
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="sql-server-2012-sp2-release-notes"></a>SQL Server 2012 SP2 Release Notes
這些版本資訊描述您在安裝或疑難排解 SQL Server 2012 Service Pack 2 之前需要了解的問題。 版本資訊僅於線上提供，安裝媒體中並不提供。 我們會在發現問題時定期更新它們。 如需詳細資訊，請參閱 [SQL Server 2012 Service Pack 2 中修正的錯誤](http://support.microsoft.com/KB/2958429) 。  
  
## <a name="choose-the-correct-file-to-download-and-install"></a>選擇正確檔案來下載並安裝  
使用下表，根據您目前安裝的版本來識別要下載的檔案位置與名稱。 下載頁面會提供系統需求與基本安裝指示。  
  
||||  
|-|-|-|  
|**目前安裝的版本為...**|**而您要...**|**請下載並安裝...**|  
|32 位元安裝：|||  
|任何 SQL Server 2012 版本的 32 位元版本|升級為 32 位元版本的 SQL Server 2012 SP2|**SQL Server 2012 SP2 下載頁面**<arch>**-**<lang id>**的** SQLServer2012SP2-KB2958429- [.exe](http://go.microsoft.com/fwlink/?LinkID=401006)|  
|32 位元版本的 SQL Server 2012 RTM Express|升級為 32 位元版本的 SQL Server 2012 Express SP2|**SQL Server 2012 SP2 Express 下載頁面**<arch>**的**<lang>**SQLEXPR_** SQLServer2012SP2-KB2958429- [.msi](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|32 位元版本的 SQL Server 2012 用戶端和管理能力工具 (包括 SQL Server 2012 Management Studio)|將用戶端和管理能力工具升級為 32 位元版本的 SQL Server 2012 SP2|**SQL Server 2012 SP2 Express 下載頁面**<arch>**的**<lang>**SQLEXPR_** SQLServer2012SP2-KB2958429- [.msi](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|32 位元版本的 SQL Server 2012 Management Studio Express|升級為 32 位元版本的 SQL Server 2012 SP2 Management Studio Express|**SQL Server 2012 SP2 Express 下載頁面**<arch>**的**<lang>**SQLEXPR_** SQLServer2012SP2-KB2958429- [.msi](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|32 位元版本的任何 SQL Server 2012 版本，以及 32 位元版本的用戶端和管理能力工具 (包括 SQL Server 2012 RTM Management Studio)|將所有產品升級為 32 位元版本的 SQL Server 2012 SP2|**SQL Server 2012 SP2 Express 下載頁面**<arch>**的**<lang>**SQLEXPRADV_** _ [.msi](http://go.microsoft.com/fwlink/?LinkID=401007)。|  
|來自 [Microsoft SQL Server 2012 RTM 功能套件](http://www.microsoft.com/download/details.aspx?id=29065) 或 [Microsoft SQL Server 2012 SP1 功能套件](http://go.microsoft.com/fwlink/p/?LinkID=268266)的一或多個 32 位元版本的工具|將工具升級為 32 位元版本的 Microsoft SQL Server 2012 SP2 功能套件|來自 Microsoft [SQL Server 2012 SP2 功能套件下載頁面](http://go.microsoft.com/fwlink/?LinkID=401008)的一個或多個工具|  
|64 位元安裝：|||  
|任何 SQL Server 2012 版本的 64 位元版本|升級為 64 位元版本的 SQL Server 2012 SP2|來自<arch>-<langid>SQL Server 2012 SP2 下載頁面 [的 SQLServer2012SP2-KB2958429-](http://go.microsoft.com/fwlink/?LinkID=401006).exe|  
|64 位元版本的 SQL Server 2012 RTM Express|升級為 64 位元版本的 SQL Server 2012 SP2|**SQL Server 2012 SP2 Express 下載頁面**<arch>**的**<lang>**SQLEXPR_** SQLServer2012SP2-KB2958429- [.msi](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|64 位元版本的 SQL Server 2012 用戶端和管理能力工具 (包括 SQL Server 2012 Management Studio)|將用戶端和管理能力工具升級為 64 位元版本的 SQL Server 2012 SP2|**SQL Server 2012 SP2 Express 下載頁面**<arch>**的**<lang>**SQLEXPR_** SQLServer2012SP2-KB2958429- [.msi](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|64 位元版本的 SQL Server 2012 Management Studio Express|升級為 64 位元版本的 SQL Server 2012 SP2 Management Studio Express|**SQL Server 2012 SP2 Express 下載頁面**<arch>**的**<lang>**SQLEXPR_** SQLServer2012SP2-KB2958429- [.msi](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|來自 [Microsoft SQL Server 2012 RTM 功能套件](http://www.microsoft.com/download/details.aspx?id=29065) 或 [Microsoft SQL Server 2012 SP1 功能套件](http://go.microsoft.com/fwlink/p/?LinkID=268266)的一或多個 64 位元版本的工具|將工具升級為 64 位元版本的 Microsoft SQL Server 2012 SP2 功能套件|來自 Microsoft [SQL Server 2012 SP2 功能套件下載頁面](http://go.microsoft.com/fwlink/?LinkID=401008)的一個或多個工具|  
  

