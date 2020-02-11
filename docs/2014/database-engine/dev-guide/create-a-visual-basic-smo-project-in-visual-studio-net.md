---
title: 在 Visual Studio .NET 中建立 Visual Basic SMO 專案 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Visual Basic [SMO]
ms.assetid: d7a3892c-0f1c-4c4d-8480-b58dce3720bc
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 662916720b9953e0374bedb29890a36ced0cfac0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62753335"
---
# <a name="create-a-visual-basic-smo-project-in-visual-studio-net"></a>在 Visual Studio .NET 中建立 Visual Basic SMO 專案
  本節描述如何建立簡單的 SMO 主控台應用程式。  
  
 此範例會匯入命名空間，讓程式可以參考 SMO 類型。 
  `Agent` 命名空間的匯入是選擇性的。 請在撰寫使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 的程式時使用該命名空間。 若要與 `Common` 的執行個體建立安全的連接，必須使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 命名空間。 
  `SqlClient` 命名空間是用於處理 SQL 例外狀況錯誤。  
  
### <a name="creating-a-visual-basic-smo-project-in-visual-studionet"></a>在 Visual Studio .NET 中建立 Visual Basic SMO 專案  
  
1.  啟動 [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)] (或 [!INCLUDE[vsprvslong](../../includes/vsprvslong-md.md)])。  
  
2.  在 [檔案]**** 功能表上，按一下 [新增專案]****。 此時會出現 [新增專案]**** 對話方塊。  
  
3.  在 [**專案類型**] 對話方塊中，選取 [ **Visual Basic**]，然後選取 [ **Windows**]。 在 [ [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]已安裝的範本] 窗格中，選取 [**主控台應用程式]。**  
  
4.  選擇性在 [**名稱**] 欄位中，輸入新應用程式的名稱。  
  
5.  按一下 **[確定]** 以[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]載入主控台應用程式範本。  
  
6.  在 [專案]**** 功能表上，選取 [新增參考]****。 [新增參考]**** 對話方塊隨即出現。  
  
7.  按一下 **[流覽]**，在 C:\PROGRAM Files\Microsoft SQL Server\120\SDK\Assemblies 資料夾中找出 SMO 元件，然後選取下列檔案。 以下是建立 SMO 應用程式所需最少的檔案：  
  
     Microsoft.SqlServer.ConnectionInfo.dll  
  
     Microsoft.SqlServer.SqlEnum.dll  
  
     Microsoft.SqlServer.Smo.dll  
  
     Microsoft.SqlServer.Management.Sdk.Sfc  
  
    > [!NOTE]  
    >  使用 `Ctrl` 鍵以選取一個以上的檔案。  
  
8.  加入任何需要的其他 SMO 組件。 例如，如果要特別開發 [!INCLUDE[ssSB](../../includes/sssb-md.md)]，請加入下列組件：  
  
     Microsoft.SqlServer.ServiceBrokerEmum.dll  
  
9. 按一下 **[開啟]** 。  
  
10. 在 [ **View** ] 功能表上，按一下 [程式**代碼**]。-或-選取 [Module1] 視窗以顯示程式碼視窗。  
  
11. 在程式碼的任何宣告之前，輸入下列**Imports**語句，以限定 SMO 命名空間中的類型。  
  
    ```  
    Imports Microsoft.SqlServer.Management.Smo  
    Imports Microsoft.SqlServer.Management.Common  
    ```  
  
12. SMO 在 Microsoft.SqlServer.Management.Smo 之下具有多個命名空間，例如 Microsoft.SqlServer.Management.Smo.Agent。 需要時才新增命名空間。  
  
13. 您現在可以加入您的 SMO 程式碼。  
  
  
