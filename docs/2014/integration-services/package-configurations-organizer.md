---
title: 封裝組態組合管理 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.packageconfigurationorganizer.f1
helpviewer_keywords:
- Package Configurations Organizer dialog box
ms.assetid: f20ae6cb-9e6a-4d24-88ff-d7a903a4e8d3
caps.latest.revision: 37
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 474a79d94d08aa477bc30241a3309c7b9f5dfed3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36135217"
---
# <a name="package-configurations-organizer"></a>[封裝組態組合管理]
  使用 **[封裝組態組合管理]** 對話方塊，即可啟用封裝組態、檢視目前封裝的組態清單，以及指定載入組態的喜好順序。  
  
> [!NOTE]  
>  組態可用於封裝部署模型。 參數是用來取代專案部署模型的組態。 專案部署模型讓您能將 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案部署到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 伺服器。 如需有關部署模型的詳細資訊，請參閱＜ [Deployment of Projects and Packages](packages/deploy-integration-services-ssis-projects-and-packages.md)＞。  
  
 如果組態更新相同的屬性，列於組態清單較下面的組態值會取代清單中較上面的組態值。 載入屬性的最後一個值是封裝執行時所使用的值。 此外，如果封裝使用如 XML 組態檔案等直接組態以及如環境變數等間接組態的組合，則指向直接組態位置的間接組態必須是清單中較上面的部份。  
  
> [!NOTE]  
>  以喜好的順序載入封裝組態時，組態會根據 **[封裝組態組合管理]** 對話方塊中清單顯示的順序 (由上而下) 依序載入。 不過，在執行階段，封裝組態可能不會以喜好的順序載入。 特別是，父封裝組態會在其他類型的組態後面載入。  
  
 封裝組態會在執行階段更新封裝物件的屬性值。 載入封裝時，組態值將會取代開發封裝時所設定的值。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 支援不同的組態類型。 例如，您可以使用包含多個組態的 XML 檔案，或是包含單一組態的環境變數。 如需相關資訊，請參閱 [Package Configurations](../../2014/integration-services/package-configurations.md)。  
  
## <a name="options"></a>選項。  
 **啟用封裝組態**  
 選取即可使用封裝的組態。  
  
 **組態名稱**  
 檢視組態的名稱。  
  
 **組態類型**  
 檢視儲存組態的位置類型。  
  
 **組態字串**  
 檢視儲存組態值的位置。 位置可以是檔案的路徑、環境變數的名稱、父封裝變數的名稱、登錄機碼，或是 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料表的名稱。  
  
 **目標物件**  
 檢視組態所更新之物件的名稱。 如果組態是 XML 組態檔或 SQL Server 資料表，則資料行是空白的，因為該組態可包含多個物件。  
  
 **目標屬性**  
 檢視組態所修改之屬性的名稱。 如果組態類型支援多個組態，則此資料行是空白。  
  
 **[加入]**  
 使用封裝組態精靈來加入組態。  
  
 **編輯**  
 重新執行封裝組態精靈來編輯現有的組態。  
  
 **移除**  
 選取組態，然後按一下 [移除]。  
  
 **箭頭**  
 選取組態，然後使用向上和向下箭頭，即可將其在清單中向上移動或向下移動。 組態會依其出現在清單中的順序載入。  
  
## <a name="see-also"></a>另請參閱  
 [建立封裝組態](../../2014/integration-services/create-package-configurations.md)  
  
  