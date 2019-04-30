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
ms.openlocfilehash: 94466dc6c069ced5b2743cbd8a14d98271303477
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63188854"
---
# <a name="start-sql-server-management-studio"></a>啟動 SQL Server Management Studio
  在開始這個教學課程之前，我們先看一下 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
## <a name="opening-sql-server-management-studio"></a>開啟 SQL Server Management Studio  
  
#### <a name="to-open-sql-server-management-studio"></a>開啟 SQL Server Management Studio  
  
1.  在上**開始**功能表上，指向**所有程式**，指向[!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]，然後按一下**SQL Server Management Studio**。  
  
    > [!NOTE]  
    >  預設不會安裝 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 如果沒有 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]，請執行安裝程式來安裝它。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 未提供 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] Express 可從免費下載[Microsoft 下載中心](https://go.microsoft.com/fwlink/?LinkID=37075&clcid=0x409)，但有不同的使用者介面與本教學課程中所述。  
  
2.  在 [連接到伺服器] 對話方塊中，驗證預設值，然後按一下 [連接]。 若要連接，**伺服器名稱**方塊必須包含電腦的名稱，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝。 如果[!INCLUDE[ssDE](../../includes/ssde-md.md)]具名執行個體，**伺服器名稱**方塊也應該包含執行個體名稱格式\< *computer_name* > \\ <*instance_name*>。  
  
## <a name="management-studio-components"></a>Management Studio 元件  
 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 在特定資訊類型專用的視窗中呈現資訊。 資料庫資訊是顯示在「物件總管」和文件視窗中。  
  
-   物件總管是含有伺服器中所有資料庫物件的樹狀檢視。 其中可包括 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]和 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]的資料庫。 物件總管含有它所連接的所有伺服器的資訊。 當您開啟 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]時，系統會提示您將物件總管連接到上次使用的設定。 您可以在 [已註冊的伺服器] 元件中，按兩下任何伺服器來連接它，但您不需要註冊要連接的伺服器。  
  
-   文件視窗是 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]最大的部分。 文件視窗可包含查詢編輯器和瀏覽器視窗。 預設會顯示目前電腦中 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體所連接的 [摘要] 頁面。  
  
## <a name="showing-additional-windows"></a>顯示其他視窗  
  
#### <a name="to-show-the-registered-servers-window"></a>顯示 [已註冊的伺服器] 視窗  
  
1.  在 [檢視] 功能表上，按一下 [已註冊的伺服器]。  
  
     [已註冊的伺服器] 視窗會出現在「物件總管」上方。 [已註冊的伺服器] 會列出您經常管理的伺服器。 您可以在這份清單中，新增和移除伺服器。 列出的伺服器只包括您執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之電腦中的 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 執行個體。  
  
2.  如果您的伺服器不會出現，在 已註冊的伺服器，以滑鼠右鍵按一下**Database Engine**，然後按一下**更新本機伺服器註冊**。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [連接已註冊的伺服器和物件總管](../object/object-explorer.md)  
  
  
