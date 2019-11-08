---
title: 啟動 SQL Server Management Studio | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 25ffaea6-0eee-4169-8dd0-1da417c28fc6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bd7fed6fff4ddd55ef56e4c5b342c56b6c2f462f
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/05/2019
ms.locfileid: "73632791"
---
# <a name="start-sql-server-management-studio"></a>啟動 SQL Server Management Studio
  在開始這個教學課程之前，我們先看一下 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
## <a name="opening-sql-server-management-studio"></a>開啟 SQL Server Management Studio  
  
#### <a name="to-open-sql-server-management-studio"></a>開啟 SQL Server Management Studio  
  
1.  在 [**開始**] 功能表上，依序指向 [**所有程式**] 和 [[!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]]，然後按一下 [ **SQL Server Management Studio**]。  
  
    > [!NOTE]  
    >  預設不會安裝 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 如果沒有 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]，請執行安裝程式來安裝它。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 未提供 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] Express 可從[Microsoft 下載中心](https://www.microsoft.com/download/details.aspx?id=7593)免費下載，但其使用者介面與本教學課程中所述的不同。  
  
2.  在 [連接到伺服器] 對話方塊中，驗證預設值，然後按一下 [連接]。 若要連接，[**伺服器名稱**] 方塊必須包含安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的電腦名稱稱。 如果 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 是已命名的實例，則 [**伺服器名稱**] 方塊也應該包含實例名稱，格式為 \<*computer_name*>\\ *<instance_name*>。  
  
## <a name="management-studio-components"></a>Management Studio 元件  
 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 在特定資訊類型專用的視窗中呈現資訊。 資料庫資訊是顯示在「物件總管」和文件視窗中。  
  
-   物件總管是含有伺服器中所有資料庫物件的樹狀檢視。 其中可包括 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]和 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]的資料庫。 物件總管含有它所連接的所有伺服器的資訊。 當您開啟 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]時，系統會提示您將物件總管連接到上次使用的設定。 您可以在 [已註冊的伺服器] 元件中，按兩下任何伺服器來連接它，但您不需要註冊要連接的伺服器。  
  
-   文件視窗是 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]最大的部分。 文件視窗可包含查詢編輯器和瀏覽器視窗。 預設會顯示目前電腦中 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體所連接的 [摘要] 頁面。  
  
## <a name="showing-additional-windows"></a>顯示其他視窗  
  
#### <a name="to-show-the-registered-servers-window"></a>顯示 [已註冊的伺服器] 視窗  
  
1.  在 [檢視] 功能表上，按一下 [已註冊的伺服器]。  
  
     [已註冊的伺服器] 視窗會出現在「物件總管」上方。 [已註冊的伺服器] 會列出您經常管理的伺服器。 您可以在這份清單中，新增和移除伺服器。 列出的伺服器只包括您執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之電腦中的 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]執行個體。  
  
2.  如果您的伺服器沒有出現，請在 [已註冊的伺服器] 中，以滑鼠右鍵按一下 [**資料庫引擎**]，然後按一下 [**更新本機伺服器註冊**]。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [連接已註冊的伺服器和物件總管](../object/object-explorer.md)  
  
  
