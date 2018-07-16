---
title: 連接到 Microsoft SQL Server Analysis Services (SSAS) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.connsqlserveras.f1
ms.assetid: 7f3244ee-b690-471c-893d-68e361c2d416
caps.latest.revision: 11
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 43a7dd31c52c81f7a2bfcbf87d1a8df3f6740081
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37323658"
---
# <a name="connect-to-microsoft-sql-server-analysis-services-ssas"></a>連接到 Microsoft SQL Server Analysis Services (SSAS)
  此頁面**資料表匯入精靈**可讓您指定從 Microsoft SQL Server Analysis Services cube 或 SharePoint 主控的 PowerPivot 活頁簿匯入資料的設定。 若要從 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]存取精靈，請按一下 **[模型]** 功能表上的 **[從資料來源匯入]**。  
  
 若要連接至資料來源，您必須先在電腦上安裝適當的提供者。  
  
> [!NOTE]  
>  在這個頁面中選取資料庫時，會使用目前使用者的認證。 不過，如果在 [模擬資訊] 頁面中指定的使用者未具備從所選取資料庫讀取的權限，則匯入將不會成功。  
  
## <a name="uielement-list"></a>UIElement 清單  
 **易記連接名稱**  
 為此資料來源連接輸入唯一的名稱。 這是必要的欄位。  
  
 **伺服器或檔案名稱**  
 輸入下列其中一項：  
  
-   輸入要連接之 SQL Server Analysis Services 伺服器的名稱或 IP 位址。  
  
     您可以使用句號 (.)、(local) 或 localhost 表示本機伺服器。  
  
-   輸入發行至 SharePoint 之 PowerPivot 活頁簿的 URL。  
  
 **[使用 Windows 驗證]**  
 指定是否使用 Windows 驗證來連接 SQL Server Analysis Services 伺服器。  
  
 Windows 驗證模式可讓使用者透過 Windows 使用者帳戶連接。 可能的話，請使用 Windows 驗證。  
  
 如果使用 Windows 驗證，目前使用者的認證會在預覽和篩選 [資料表屬性] 視窗和 [匯入精靈] 中的資料時使用。 這些認證不會用來匯入或重新整理資料，而是會使用 [模擬資訊] 頁面上指定的 Windows 認證。  
  
 **[使用 SQL Server 驗證]**  
 指定是否使用 SQL Server 驗證來連接 SQL Server Analysis Services 伺服器。  
  
 使用 SQL Server 驗證時，SQL Server 會查看是否已經設定 SQL Server 登入帳戶，以及指定的密碼是否符合先前記錄的密碼，藉以自行執行驗證。  
  
 SQL Server 驗證是用來建構資料來源的連接字串。 這些認證也會在預覽和篩選 [資料表屬性] 視窗和 [匯入精靈] 中的資料時使用。 這些認證不會用來匯入或重新整理資料，而是會使用 [模擬資訊] 頁面上指定的 Windows 認證。  
  
 **使用者名稱**  
 為資料庫連接指定使用者名稱。 只有在您選取使用 Windows 驗證連接時，才能使用此選項。  
  
 **密碼**  
 為資料庫連接指定密碼。 只有在您選擇使用 [SQL Server 驗證] 進行連接時，才能編輯此選項。  
  
 **儲存我的密碼**  
 指定是否要儲存您在 **[密碼]** 方塊中輸入的密碼。 只有在您選擇使用 [SQL Server 驗證] 進行連接時，才能使用此選項。  
  
 **資料庫名稱**  
 從資料庫清單中選取資料庫。  
  
 **進階**  
 使用 **[設定進階屬性]** 對話方塊設定其他連接屬性。 如需詳細資訊，請參閱[設定進階屬性 &#40;SSAS&#41;](set-advanced-properties-ssas.md)。  
  
 **測試連接**  
 嘗試使用目前的設定建立與資料來源之間的連接。 顯示一則訊息，指出連接是否成功。  
  
  
