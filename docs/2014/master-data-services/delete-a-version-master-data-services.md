---
title: 刪除版本 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- versions [Master Data Services], deleting
- deleting versions [Master Data Services]
ms.assetid: 2a4eeffe-8379-4744-ad44-c27d8c8ac9a8
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: d75d6719219a41dfc42071a82375a66bdd877a57
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62925013"
---
# <a name="delete-a-version-master-data-services"></a>刪除版本 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，當您確定不再需要與某個版本有關的主要資料時，可刪除此版本。 當您刪除版本之後，就無法擷取關聯的主要資料。  
  
> [!WARNING]  
>  如果模型只有一個版本而且您將它刪除，此模型就無法使用。  
  
## <a name="prerequisites"></a>先決條件  
 若要執行此程序：  
  
-   您在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫中，必須擁有檢視 mdm.viw_SYSTEM_SCHEMA_VERSION 檢視表的權限以及執行 mds.udpVersionDelete 預存程序的權限。 如需詳細資訊，請參閱[資料庫物件安全性 &#40;Master Data Services&#41;](database-object-security-master-data-services.md)。  
  
### <a name="to-delete-a-version"></a>若要刪除版本  
  
1.  開啟 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 並且連接到 [!INCLUDE[ssDE](../includes/ssde-md.md)] 資料庫的 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 執行個體。  
  
2.  開啟 mdm.viw_SYSTEM_SCHEMA_VERSION 檢視表。  
  
3.  尋找您想要刪除之模型的版本，然後將值複製到 **[識別碼]** 欄位。  
  
4.  建立新的查詢。  
  
5.  輸入下列文字，使用您在步驟 2 複製的值取代 *version_ID* 。  
  
    ```  
    EXEC [mdm].[udpVersionDelete] @Version_ID='version_ID'  
    ```  
  
6.  執行查詢。  
  
    > [!NOTE]  
    >  您可能需要等候幾分鐘，Web 應用程式才會反映變更。  
  
## <a name="see-also"></a>另請參閱  
 [版本 &#40;Master Data Services&#41;](../../2014/master-data-services/versions-master-data-services.md)   
 [複製版本 &#40;Master Data Services&#41;](../../2014/master-data-services/copy-a-version-master-data-services.md)  
  
  
