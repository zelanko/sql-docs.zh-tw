---
title: 針對查閱轉換來建立及部署快取 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- creating cache files for Lookup transformation
- deploying cache files for Lookup transformation
- Lookup transformation cache files
ms.assetid: cedf5cad-2fac-42d0-ad91-9461e117d330
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: f82feebd86e06fb7422cb36659645b9bc9702000
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36145431"
---
# <a name="create-and-deploy-a-cache-for-the-lookup-transformation"></a>針對查閱轉換來建立及部署快取
  您可以針對查閱轉換建立及部署快取檔案 (.caw)。 參考資料集會儲存在快取檔案中。  
  
 查閱轉換會藉由聯結已連接資料來源輸入資料行中的資料與參考資料集中的資料行來執行查閱。  
  
 您可以使用快取連接管理員和快取轉換轉換來建立快取檔案。 如需詳細資訊，請參閱 [快取連線管理員](../../connection-manager/cache-connection-manager.md) 和 [快取轉換](cache-transform.md)。  
  
 若要深入了解查閱轉換和快取檔案，請參閱 [查閱轉換](lookup-transformation.md)。  
  
### <a name="to-create-a-cache-file"></a>若要建立快取檔案  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]中，開啟包含所要封裝的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 專案，然後再開啟封裝。  
  
2.  在 [控制流程] 索引標籤上，加入資料流程工作。  
  
3.  在 [資料流程] 索引標籤上，將「快取轉換」轉換加入至資料流程，然後將該轉換連接到資料來源。  
  
     視需要設定資料來源。  
  
4.  按兩下快取轉換，然後在 [快取轉換編輯器] 中，按一下 [連線管理員] 頁面上的 [新增]，建立新的快取連線管理員。  
  
5.  在 [快取連線管理員編輯器] 的 [一般] 索引標籤上，藉由設定下列選項，將快取連線管理員設定為儲存快取：  
  
    1.  選取 [使用檔案快取]。  
  
    2.  針對 [檔案名稱]，輸入檔案路徑。  
  
     系統會在執行封裝時建立該檔案。  
  
    > [!NOTE]  
    >  封裝保護等級不會套用至快取檔案。 如果快取檔案包含機密資訊，請使用存取控制清單 (ACL) 限制對其中儲存檔案的位置或資料夾的存取權。 您應該只啟用特定帳戶的存取權。 如需詳細資訊，請參閱[對封裝使用之檔案的存取權](../../access-to-files-used-by-packages.md)。  
  
6.  按一下 [資料行] 索引標籤，然後使用 [索引位置] 選項，指定哪些資料行是索引資料行。  
  
     如果是非索引資料行，索引位置為 0。 如果是索引資料行，則索引位置是循序的正數。  
  
    > [!NOTE]  
    >  當查閱轉換是設定為使用快取連接管理員，則只有參考資料集中的索引資料行可以對應到輸入資料行。 而且，所有的索引資料行都必須進行對應。  
  
     如需詳細資訊，請參閱[快取連線管理員編輯器](../../cache-connection-manager-editor.md)。  
  
7.  視需要設定快取轉換。  
  
     如需詳細資訊，請參閱[快取轉換編輯器 &#40;連線管理員頁面&#41;](../../cache-transformation-editor-connection-manager-page.md) 和[快取轉換編輯器 &#40;對應頁面&#41;](../../cache-transformation-editor-mappings-page.md)。  
  
8.  執行封裝。  
  
### <a name="to-deploy-a-cache-file"></a>若要部署快取檔案  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]中，開啟包含所要封裝的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 專案，然後再開啟封裝。  
  
2.  選擇性地建立封裝設定。 如需詳細資訊，請參閱[建立封裝組態](../../create-package-configurations.md)。  
  
3.  藉由執行下列工作，將快取檔案加入至專案：  
  
    1.  在 [方案總管] 中，選取在步驟 1 中開啟的專案。  
  
    2.  在 [專案] 功能表上，按一下 [加入現有項目]。  
  
    3.  選取快取檔案，然後按一下 [加入]。  
  
     檔案便會出現在方案總管的 [其他] 資料夾中。  
  
4.  將專案設定為建立部署公用程式，然後建立專案。 如需詳細資訊，請參閱 [建立部署公用程式](../../create-a-deployment-utility.md)。  
  
     資訊清單檔 \<專案名稱>.SSISDeploymentManifest.xml 會建立，並列出專案中的其他檔案、封裝以及封裝組態。  
  
5.  將封裝部署到檔案系統。 如需詳細資訊，請參閱 [使用部署公用程式來部署封裝](../../deploy-packages-by-using-the-deployment-utility.md)。  
  
## <a name="see-also"></a>另請參閱  
 [建立部署公用程式](../../create-a-deployment-utility.md)  
  
  