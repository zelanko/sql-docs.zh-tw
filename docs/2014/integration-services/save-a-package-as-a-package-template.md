---
title: 將封裝儲存為封裝範本 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- reusing packages
- templates [Integration Services]
ms.assetid: efe66cec-3933-4f6e-8d35-fe3d300de66c
caps.latest.revision: 16
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: dfd90b00e413f5a25de9770bf41b094bbdb9d808
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37158499"
---
# <a name="save-a-package-as-a-package-template"></a>將封裝儲存為封裝範本
  本主題描述當您在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中建立新的 Integration Services 封裝時，如何指定及使用自訂封裝做為範本。 根據預設，當您將新封裝加入 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案中時， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 會使用可建立空白封裝的封裝範本。 您不能置換這個預設範本，但是可以加入新的範本。  
  
 您可以指定將多個封裝當作範本使用。 不過您必須先建立封裝，才能將自訂封裝實作成範本。  
  
 使用自訂封裝作為範本以建立封裝時，新封裝將擁有與範本相同的名稱和 GUID。 為了區分這些封裝，您應該更新 `Name` 屬性的值，並為 `ID` 屬性產生新的 GUID。 如需詳細資訊，請參閱 [在 SQL Server 資料工具中建立封裝](create-packages-in-sql-server-data-tools.md) 和 [設定封裝屬性](set-package-properties.md)。  
  
### <a name="to-designate-a-custom-package-as-a-package-template"></a>若要將自訂封裝指定成封裝範本  
  
1.  在檔案系統中，尋找要用來當作範本的封裝。  
  
2.  將封裝複製到 DataTransformationItems 資料夾。 依預設，這個資料夾位於 C:\Program Files\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies\ProjectItems\DataTransformationProject。  
  
3.  對想要當作範本使用的每個封裝重複步驟 1 和 2。  
  
### <a name="to-use-a-custom-package-as-a-package-template"></a>若要使用自訂封裝作為封裝範本  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，開啟您要在其中建立封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在方案總管中，以滑鼠右鍵按一下專案，指向 [加入]，然後按一下 [新增項目]。  
  
3.  在 [新增新項目 -\<專案名稱>] 對話方塊中，按一下要當作範本使用的套件。  
  
     範本清單中包含名稱為 [新增 SSIS 封裝] 的預設封裝範本。 封裝圖示識別可當作封裝範本使用的範本。  
  
4.  按一下 **[加入]**。  
  
## <a name="see-also"></a>另請參閱  
 [在 SQL Server Data Tools 中建立封裝](create-packages-in-sql-server-data-tools.md)   
 [Integration Services &#40;SSIS&#41; 封裝](../../2014/integration-services/integration-services-ssis-packages.md)  
  
  
