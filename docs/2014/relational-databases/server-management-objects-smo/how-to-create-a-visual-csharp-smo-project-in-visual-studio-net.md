---
title: '在 Visual Studio .NET 中建立 Visual c # SMO 專案 |Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- Visual C# [SMO]
ms.assetid: 1e7abb16-23a0-4a18-91ad-253261e6bf84
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 371da8231138fb43e9b001808b9fb88ad09543b5
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63131647"
---
# <a name="create-a-visual-c-smo-project-in-visual-studio-net"></a>在 Visual Studio .NET 中建立 Visual C# SMO 專案
  本節描述如何建立簡單的 SMO 主控台應用程式。  
  
 此範例會匯入命名空間，讓程式可以參考 SMO 類型。 `Agent` 命名空間的匯入是選擇性的。 請在撰寫使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 的程式時使用該命名空間。 若要與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體建立安全的連接，必須使用 `Common` 命名空間。 `SqlClient` 命名空間是用於處理 SQL 例外狀況錯誤。  
  
### <a name="creating-a-visual-c-smo-project-in-visual-studionet"></a>在 Visual Studio .NET 中建立 Visual C# SMO 專案  
  
1.  啟動 [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)] (或 [!INCLUDE[vsprvslong](../../includes/vsprvslong-md.md)])。  
  
2.  在 [檔案]**** 功能表上，按一下 [新增專案]****。 [新增專案]  對話方塊隨即出現。  
  
3.  在 [**專案類型**] 對話方塊中，選取 [ **Visual c #**]，然後選取 [ **Windows**]。 在 [ [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]已安裝的範本] 窗格中，選取 [ **Windows 應用程式**]。  
  
4.  選擇性在 [**名稱**] 欄位中，輸入新應用程式的名稱  
  
5.  選取 Visual C# 應用程式類型。 在接下來的範例中，選取 [**主控台應用程式**]。  
  
6.  在 [專案]**** 功能表上，選取 [新增參考]****。 [新增參考]**** 對話方塊隨即出現。  
  
7.  按一下 **[流覽]**，在[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]資料夾中找出 SMO 元件，然後選取下列檔案。 以下是建立 SMO 應用程式所需最少的檔案：  
  
     Microsoft.SqlServer.ConnectionInfo.dll  
  
     Microsoft.SqlServer.Smo.dll  
  
     Microsoft.SqlServer.Management.Sdk.Sfc.dll  
  
     Microsoft.SqlServer.SqlEnum.dll  
  
    > [!NOTE]  
    >  使用 `Ctrl` 鍵以選取一個以上的檔案。  
  
8.  加入任何需要的其他 SMO 組件。 例如，如果要特別開發 [!INCLUDE[ssSB](../../includes/sssb-md.md)]，請加入下列組件：  
  
     Microsoft.SqlServer.ServiceBrokerEmum.dll  
  
9. 按一下 [開啟]  。  
  
10. 在 [ **View** ] 功能表上，按一下 [程式**代碼**]。-或-選取 [Program1.cs [Design]] 視窗，然後按兩下 windows form 以顯示程式碼視窗。  
  
11. 在程式碼的命名空間陳述式之前，輸入下列 `using` 陳述式來限定 SMO 命名空間中的類型：  
  
    ```  
    using Microsoft.SqlServer.Management.Smo;  
    using Microsoft.SqlServer.Management.Common;  
    ```  
  
12. SMO 在 Microsoft.SqlServer.Management.Smo 之下具有多個命名空間，例如 Microsoft.SqlServer.Management.Smo.Agent。 需要時才新增命名空間。  
  
13. 您現在可以加入您的 SMO 程式碼。  
  
  
