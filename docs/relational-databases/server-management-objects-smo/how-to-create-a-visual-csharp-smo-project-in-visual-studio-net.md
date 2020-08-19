---
description: 如何：在 Visual Studio .NET 中建立 Visual C# SMO 專案
title: 在 Visual Studio .NET 中建立 Visual C# SMO 專案
ms.custom: seo-dt-2019
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
ms.openlocfilehash: 518e8441c19286e3a0daccca724062a8ff54294a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88420252"
---
# <a name="how-to-create-a-visual-c-smo-project-in-visual-studio-net"></a>如何：在 Visual Studio .NET 中建立 Visual C# SMO 專案
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  本節描述如何建立簡單的 SMO 主控台應用程式。  
  
 此範例會匯入命名空間，讓程式可以參考 SMO 類型。 **代理程式**命名空間的匯入是選擇性的。 請在撰寫使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 的程式時使用該命名空間。 需要 **通用** 命名空間，才能建立與實例的安全連線 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 **SqlClient**命名空間是用來處理 SQL 例外狀況錯誤。  
  
### <a name="creating-a-visual-c-smo-project-in-visual-studionet"></a>在 Visual Studio .NET 中建立 Visual C# SMO 專案  
  
1. 啟動 Visual Studio
  
2. **在 [檔案**] 功能表上，按一下 [**新增**]，然後按一下 [**專案**]。  [新增專案]  對話方塊隨即出現。   
  
3. 在 [ [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] **已安裝**] 窗格中，流覽至 [**範本** \\ **Visual c #**] \\ **視窗**並選取 [**主控台應用程式**]。  
  
4.  ([ **名稱** ] 文字方塊中的選擇性) ，輸入新應用程式的名稱。  

5. 按一下 **[確定]** 以載入主控台應用程式範本。  

6. 遵循 [安裝 SMO](installing-smo.md) 的指示，為您的專案安裝套件以供參考。
  
7. 在 [檢視]**** 功能表中，按一下 [程式碼]****。
    
8. 在程式碼的命名空間語句前面，輸入下列 **using** 語句，以限定 SMO 命名空間中的類型：
  
    ```  
    using Microsoft.SqlServer.Management.Smo;  
    using Microsoft.SqlServer.Management.Common;  
    ```  
  
15. SMO 在 Microsoft.SqlServer.Management.Smo 之下具有多個命名空間，例如 Microsoft.SqlServer.Management.Smo.Agent。 需要時才新增命名空間。  
  
16. 您現在可以加入您的 SMO 程式碼。  

