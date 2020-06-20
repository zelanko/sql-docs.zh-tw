---
title: 發行資料庫 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 98b2914e-7147-40af-ba7d-87253bbe8bf9
author: stevestein
ms.author: sstein
ms.openlocfilehash: e64cc8961b4a576e0b67a290e84afc699b4a73ef
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965798"
---
# <a name="publish-a-database-sql-server-management-studio"></a>發行資料庫 (SQL Server Management Studio)
  您可以使用 **[產生和發佈指令碼]** 精靈，將整個資料庫或個別的資料庫物件發行至 Web 主控提供者。  
  
> [!NOTE]  
>  本主題所述的功能在過去是由發行資料庫精靈所提供。 發行功能已經加入至產生和發佈指令碼精靈，而且發行資料庫精靈已經停用。  
  
## <a name="generate-and-publish-scripts-wizard"></a>[產生和發佈指令碼]  
 產生和發佈指令碼精靈可用來將資料庫或選定的資料庫物件發行至 Web 主控提供者。 SQL Server Web 主控提供者是與 Web 服務之間的連接介面。 此 Web 服務是使用 CodePlex 上 SQL Server Hosting Toolkit 中的資料庫發行服務專案所建立。 此 Web 服務可讓 Web 主控者客戶輕鬆地使用產生和發佈指令碼精靈，將他們的資料庫發行到此服務。 如需有關下載 SQL Server Hosting Toolkit 的詳細資訊，請參閱 [SQL Server 資料庫發行服務](https://go.microsoft.com/fwlink/?LinkId=142025)。  
  
 產生和發佈指令碼精靈也可以用來建立傳輸資料庫的指令碼。  
  
#### <a name="to-publish-a-database-to-a-web-service"></a>若要將資料庫發行到 Web 服務  
  
1.  在物件總管中，展開 [資料庫]  ，以滑鼠右鍵按一下資料庫，指向 [工作]  ，然後按一下 [產生和發佈指令碼]  。 遵循精靈中的步驟，以便編寫要發行之資料庫物件的指令碼。  
  
2.  在 **[選擇物件]** 頁面上，選取要發行至 Web 主控服務的物件。  
  
3.  在 **[設定指令碼編寫選項]** 頁面上，選取 **[發佈到 Web 服務]** 。  
  
    1.  在 **[提供者]** 方塊中，指定您的 Web 服務提供者。 如果您尚未設定 Web 主控提供者，請選取 **[管理提供者]** ，並使用 **[管理提供者]** 對話方塊來設定 Web 服務的提供者。  
  
    2.  若要指定進階發行選項，請選取 **[發佈到 Web 服務]** 區段中的 **[進階]** 按鈕。  
  
4.  在 **[摘要]** 頁面中，檢閱您的選取。 按 **[上一步]** 可變更您的選取。 按 **[下一步]** ，發佈您選取的物件。  
  
5.  在 **[儲存或發佈指令碼]** 頁面上，監視發行的進度。  
  
## <a name="see-also"></a>另請參閱  
 [產生指令碼 &#40;SQL Server Management Studio&#41;](../scripting/generate-scripts-sql-server-management-studio.md)   
 [複製資料庫至其他伺服器](copy-databases-to-other-servers.md)  
  
  
