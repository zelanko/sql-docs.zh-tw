---
title: 連接到 Microsoft SQL Server 資料庫 (SSAS) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.connsqlserverdb.f1
ms.assetid: 6ebfe029-dbba-4f0d-a556-328e79ef629f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6e3015f589f40dfc8bafc30da3a30316004f086a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62680179"
---
# <a name="connect-to-a-microsoft-sql-server-database-ssas"></a>連接到 Microsoft SQL Server 資料庫 (SSAS)
  **[資料表匯入精靈]** 的這個頁面可讓您指定連接到 Microsoft SQL Server 資料庫的設定。 若要從 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]存取精靈，請按一下 **[模型]** 功能表上的 **[從資料來源匯入]**。  
  
 若要連接至資料來源，您必須先在電腦上安裝適當的提供者。  
  
> [!NOTE]  
>  在這個頁面中選取資料庫時，會使用目前使用者的認證。 不過，如果在 [模擬資訊] 頁面中指定的使用者未具備從所選取資料庫讀取的權限，則匯入將不會成功。  
  
## <a name="uielement-list"></a>UIElement 清單  
 **易記連接名稱**  
 為此資料來源連接輸入唯一的名稱。 這是必要的欄位。  
  
 **伺服器名稱**  
 選取要連接之 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體的名稱，或輸入它的名稱或 IP 位址。  
  
 您可以使用句號 (.)、(local) 或 localhost 表示本機伺服器。  
  
 **[使用 Windows 驗證]**  
 指定是否使用 Windows 驗證來連接 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的執行個體。  
  
 Windows 驗證模式可讓使用者透過 Windows 使用者帳戶進行連接。 可能的話，請使用 Windows 驗證。  
  
 如果使用 Windows 驗證，目前使用者的認證會在預覽和篩選 [資料表屬性] 視窗和 [匯入精靈] 中的資料時使用。 這些認證不會用來匯入或重新整理資料，而是會使用 [模擬資訊] 頁面上指定的 Windows 認證。  
  
 **[使用 SQL Server 驗證]**  
 指定是否使用 SQL Server 驗證來連接 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的執行個體。  
  
 使用 SQL Server 驗證時，SQL Server 會查看是否已經設定 SQL Server 登入帳戶，以及指定的密碼是否符合先前記錄的密碼，藉以自行執行驗證。  
  
 SQL Server 驗證是用來建構資料來源的連接字串。 這些認證也會在預覽和篩選 [資料表屬性] 視窗和 [匯入精靈] 中的資料時使用。 這些認證不會用來匯入或重新整理資料，而是會使用 [模擬資訊] 頁面上指定的 Windows 認證。  
  
 **使用者名稱**  
 為資料庫連接指定使用者名稱。 只有在您選擇使用 [SQL Server 驗證] 進行連接時，才能使用此選項。  
  
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
  
  
