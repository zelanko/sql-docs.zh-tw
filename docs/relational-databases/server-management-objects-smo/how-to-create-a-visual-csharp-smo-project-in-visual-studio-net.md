---
title: 在 Visual Studio .NET C#中建立 Visual SMO 專案 |Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- Visual C# [SMO]
ms.assetid: 1e7abb16-23a0-4a18-91ad-253261e6bf84
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3989c49d800a9f485c8562aed4406c57216eed77
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/25/2019
ms.locfileid: "72909801"
---
# <a name="how-to-create-a-visual-c-smo-project-in-visual-studio-net"></a>如何：在 Visual Studio .NET 中建立 Visual C# SMO 專案
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  本節描述如何建立簡單的 SMO 主控台應用程式。  
  
 此範例會匯入命名空間，讓程式可以參考 SMO 類型。 **代理程式**命名空間的匯入是選擇性的。 請在撰寫使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 的程式時使用該命名空間。 必須要有**通用**命名空間，才能建立與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]實例的安全連線。 **SqlClient**命名空間是用來處理 SQL 例外狀況錯誤。  
  
### <a name="creating-a-visual-c-smo-project-in-visual-studionet"></a>在 Visual Studio .NET 中建立 Visual C# SMO 專案  
  
1. 啟動 Visual Studio
  
2. **在 [檔案**] 功能表上，依序按一下 [**新增**] 和 [**專案**]。  [新增專案] 對話方塊隨即出現。   
  
3. 在 [[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]**已安裝**] 窗格中，流覽至 [**範本**\\ **C# Visual**\\**Windows** ]，然後選取 [**主控台應用程式**]。  
  
4. 選擇性在 [**名稱**] 文字方塊中，輸入新應用程式的名稱。  

5. 按一下 **[確定]** 以載入主控台應用程式範本。  

6. 依照[安裝 SMO](installing-smo.md)上的指示來安裝套件，以供您的專案參考。
  
7. 在 [檢視] 功能表中，按一下 [程式碼]。
    
8. 在程式碼中，于 namespace 語句之前，輸入下列**using**語句來限定 SMO 命名空間中的類型：
  
    ```  
    using Microsoft.SqlServer.Management.Smo;  
    using Microsoft.SqlServer.Management.Common;  
    ```  
  
15. SMO 在 Microsoft.SqlServer.Management.Smo 之下具有多個命名空間，例如 Microsoft.SqlServer.Management.Smo.Agent。 需要時才新增命名空間。  
  
16. 您現在可以加入您的 SMO 程式碼。  

