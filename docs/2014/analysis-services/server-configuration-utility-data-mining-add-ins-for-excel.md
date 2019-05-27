---
title: 伺服器組態公用程式 （資料採礦適用於 Excel 的增益集） |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 28435f86-5cec-4a1e-9b7d-b2069c1ddddb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bdc8434673d9220f22d31f1736bd67012653dc88
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66069065"
---
# <a name="server-configuration-utility-data-mining-add-ins-for-excel"></a>伺服器組態公用程式 (適用於 Excel 的資料採礦增益集)
  當您安裝適用於 Excel 的資料採礦增益集時，伺服器組態公用程式也會安裝，而且會執行第一次您開啟增益集。本主題描述如何使用公用程式來連接到的執行個體[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]並設定適用於使用資料採礦模型的資料庫。  
  

  
##  <a name="bkmk_step1"></a> 步驟 1：連接到 Analysis Services  
 選擇提供資料採礦演算法並儲存資料採礦模型的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 伺服器。  
  
 當您建立啟用資料採礦的連接時，應該選擇可以試驗各種資料採礦模型的伺服器。 建議您在伺服器上建立新的資料庫，並且將其做為資料採礦專用的資料庫，或是請系統管理員為您準備資料採礦伺服器。 如此您就能在不影響其他服務之效能的情況下建立模型。  
  
 請注意，用於資料採礦的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 伺服器不需要與來源資料位於相同的伺服器上。  
  
 **伺服器名稱**  
 輸入伺服器名稱，此伺服器包含將用於資料採礦的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體。  
  
 **驗證**  
 指定驗證方法。 除非您的系統管理員已設定透過 HTTPPump 存取伺服器，否則需要使用 Windows 驗證才能連接到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]。  
  
##  <a name="bkmk_step2"></a> 步驟 2：允許暫時性模型  
 您必須先將 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 伺服器屬性變更為允許暫時性採礦模型，才能使用增益集。  
  
 暫時性採礦模型也稱為*工作階段模型*。 這是因為這些模型只能在您目前的工作階段開啟時儲存。 當您關閉與伺服器的連接時，工作階段會結束，而工作階段期間所使用的任何模型都會遭到刪除。  
  
 工作階段採礦模型的使用不會影響伺服器上的儲存空間，但與建立資料採礦模型相關的負擔可能會影響伺服器效能。  
  
 精靈首先會偵測您所指定之伺服器上的設定。 如果伺服器已允許暫時性採礦模型，您可以按一下**下一步**以繼續。 此精靈還提供如何在指定的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 伺服器上啟用暫時性採礦模型的指示，或是如何對您的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 系統管理員提出要求。  
  
##  <a name="bkmk_step3"></a> 步驟 3：為增益集使用者建立資料庫  
 在安裝和組態精靈的這個頁面上，您可以建立資料採礦專用的新資料庫，或選取現有的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫。  
  
> [!WARNING]  
>  資料採礦需要在多維度模式下執行的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體。 表格式模式不支援資料採礦。  
  
 建議您建立資料採礦專用的個別資料庫。 這可讓您試驗各種資料採礦模型，而不會影響其他方案物件。  
  
 如果您選擇 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體上現有的資料庫，請注意，如果您使用增益集建立模型，而已有該名稱的模型存在，則可能會覆寫現有的模型。  
  
 **建立新的資料庫**  
 選取這個選項可在選取的伺服器上建立新的資料庫。 資料採礦資料庫將儲存您的資料來源、採礦結構和採礦模型。  
  
 **資料庫名稱**  
 輸入新資料庫的名稱。 如果此名稱尚未使用，則會自動建立。  
  
 **使用現有的資料庫**  
 選取此選項可使用現有的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫。  
  
 **[資料庫備份]**  
 如果您已選擇此選項使用現有的資料庫，則必須從清單中選取資料庫名稱。  
  
##  <a name="bkmk_step4"></a> 步驟 4:授與增益集使用者適當的權限  
 您必須確定您 (和增益集的其他使用者) 必須具有必要的權限，才能瀏覽、編輯、處理或建立資料採礦結構和模型。  
  
 根據預設，使用增益集需要有整合式 Windows 驗證。  
  
 **授與增益集使用者資料庫管理權限**  
 選取此選項，為列出的使用者提供資料庫的管理權限。  
  
> [!NOTE]  
>  這些權限只適用於資料庫中所列**資料庫名稱** 方塊中。  
  
 **資料庫名稱**  
 顯示選取之資料庫的名稱。  
  
 **指定要加入的使用者或群組**  
 選取將可存取用於資料採礦之資料庫的登入帳戶。  
  
 **[加入]**  
 按一下此選項，開啟對話方塊並加入使用者或群組。  
  
 **移除**  
 按一下此選項，從使用者清單中移除具有管理權限的使用者或群組。  
  
  
