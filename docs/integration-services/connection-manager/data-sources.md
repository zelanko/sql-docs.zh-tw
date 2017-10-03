---
title: "資料來源 |Microsoft 文件"
ms.custom: 
ms.date: 08/27/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data sources [Integration Services], about data sources
ms.assetid: 7ac81612-9822-470f-8d0f-a1dc96142fe3
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 77ca3b5849eb90d21da55989d2c9ec7ae94a53f6
ms.contentlocale: zh-tw
ms.lasthandoff: 09/27/2017

---
# <a name="data-sources"></a>資料來源
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 包含您可以在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝中使用的設計階段物件：資料來源。  
  
 資料來源物件是連接的參考，且至少包含連接字串和資料來源識別碼。 它也可以包含描述、名稱、使用者名稱和密碼等其他中繼資料。  
  
> **注意：** 您只能將資料來源加入到設定為使用套件部署模型的專案。 若專案設定為使用專案部署模型，您就可以使用在專案層級建立的連接管理員來共用連接，取代使用資料來源的方式。  
>   
>  如需有關部署模型的詳細資訊，請參閱＜ [Deployment of Projects and Packages](../packages/deploy-integration-services-ssis-projects-and-packages.md)＞。 如需將專案轉換為專案部署模型的詳細資訊，請參閱 [將專案部署至 Integration Services 伺服器](https://msdn.microsoft.com/library/hh231102.aspx)。  
  
 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝中使用資料來源的好處包括：  
  
-   資料來源有專案範圍，這表示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案中建立的資料來源可使用於專案中的所有封裝。 資料來源只要定義一次，即可由多個封裝中的連接管理員參考。  
  
-   資料來源提供資料來源物件與其封裝參考之間的同步處理。 如果資料來源與參考資料來源的封裝位於同一專案，則資料來源參考的連接字串屬性便會在資料來源變更時自動更新。  
  
## <a name="reference-data-sources"></a>參考資料來源  
 如果要將資料來源物件加入 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案，請以滑鼠右鍵按一下**方案總管**中的 [資料來源] 資料夾，然後按一下 [新增資料來源]。 項目會隨即加入至 [資料來源] 資料夾。 如果您要使用在其他專案中建立的資料來源物件，您必須先將物件加入專案。  
  
 如果您要在封裝中使用資料來源物件，可以將參考該資料來源物件的連接管理員新增至封裝中。 在建立封裝控制流程及資料流程之前，或作為建構控制流程或資料流程程序中的一個步驟，將它新增至封裝中。  
  
 資料來源物件代表至資料來源的簡單連接，並提供其參考之資料存放區中物件的存取權。 例如，連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]AdventureWorks 範例資料庫的資料來源物件包含資料庫中的所有 60 個資料表。  
  
 資料來源與參考資料來源的連接管理員之間沒有相依性。 如果資料來源不再是專案的一部分，封裝將繼續有效，因為有關資料來源的資訊 (例如其連接類型和連接字串) 都包含在封裝定義中。  
  
  

