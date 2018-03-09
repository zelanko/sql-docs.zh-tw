---
title: "在 Visual Studio.NET 中建立 Visual C# SMO 專案 |Microsoft 文件"
ms.custom: 
ms.date: 08/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- Visual C# [SMO]
ms.assetid: 1e7abb16-23a0-4a18-91ad-253261e6bf84
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 220c190a88a1b5c5d38591905e9bb1060a2f4509
ms.sourcegitcommit: cb2f9d4db45bef37c04064a9493ac2c1d60f2c22
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/12/2018
---
# <a name="how-to-create-a-visual-c-smo-project-in-visual-studio-net"></a>如何在 Visual Studio.NET 中建立 Visual C# SMO 專案
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  本節描述如何建立簡單的 SMO 主控台應用程式。  
  
 此範例會匯入命名空間，讓程式可以參考 SMO 類型。 匯入**代理程式**是選擇性的命名空間。 請在撰寫使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 的程式時使用該命名空間。 **常見**建立的執行個體的安全連接所需的命名空間[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 **SqlClient**命名空間用來處理 SQL 例外狀況錯誤。  
  
### <a name="creating-a-visual-c-smo-project-in-visual-studionet"></a>在 Visual Studio .NET 中建立 Visual C# SMO 專案  
  
1. 啟動 Visual Studio
  
2. 在**檔案**功能表上，按一下 **新增**然後**專案**。  [新增專案]  對話方塊隨即出現。   
  
3. 在[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]**已安裝** 窗格中，瀏覽至**範本**\\**Visual C#**\\**Windows**選取**主控台應用程式**。  
  
4. （選擇性）在**名稱**文字方塊中，輸入新的應用程式的名稱。  

5. 按一下**確定**載入主控台應用程式範本。  

6. 按照指示[安裝 SMO](installing-smo.md)安裝您的專案參考的封裝。
  
7. 在 [檢視] 功能表中，按一下 [程式碼]。
    
8. 在程式碼的命名空間陳述式之前，輸入下列命令**使用**陳述式來限定 SMO 命名空間中的類型：
  
    ```  
    using Microsoft.SqlServer.Management.Smo;  
    using Microsoft.SqlServer.Management.Common;  
    ```  
  
15. SMO 在 Microsoft.SqlServer.Management.Smo 之下具有多個命名空間，例如 Microsoft.SqlServer.Management.Smo.Agent。 需要時才新增命名空間。  
  
16. 您現在可以加入您的 SMO 程式碼。  
  
  
