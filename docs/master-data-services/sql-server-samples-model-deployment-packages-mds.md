---
title: "SQL Server 範例：模型部署套件 (MDS) | Microsoft Docs"
ms.custom: 
ms.date: 07/28/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- Master Data Services
- "範例"
ms.assetid: 9b31b7b6-319b-4840-b67d-eb383e7762b1
caps.latest.revision: "21"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c438ae5bb2a00c20df66ba80211f99e7b14d51cd
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="sql-server-examples-model-deployment-packages-mds"></a>SQL Server 範例：模型部署套件 (MDS)
  當您安裝 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]時，可取得包含資料的範例模型套件。 這些套件檔案的預設位置是 \<磁碟機\Program Files\Microsoft SQL Server\130\Master Data Services\Samples\Packages。  
  
 如需如何部署範例模型套件的指示，請參閱 [部署範例模型和資料](../master-data-services/master-data-services-installation-and-configuration.md#deploySample)。 您可以使用 [MDSModelDeploy 工具](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)來部署範例模型套件。  
  
> [!IMPORTANT]  
>  **範例更新 - [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]**  
>   
>  範例套件已經過更新，可支援下列新的功能。  
>   
>  -   顯示多對多關聯性。  
>   
>      如需詳細資訊，請參閱 [範例模型中的 M2M 關聯性](../master-data-services/show-many-to-many-relationships-in-derived-hierarchies-master-data-services.md#M2MSample)。  

> -   限制網域屬性允許的值。  
>   
>      如需詳細資訊，請參閱[建立網域屬性 &#40;Master Data Services&#41;](../master-data-services/create-a-domain-based-attribute-master-data-services.md)。  
> -   需要核准實體變更。  
>   
>      如需詳細資訊，請參閱[需要核准 &#40;Master Data Services&#41;](../master-data-services/approval-required-master-data-services.md)。  
> -   在商務規則中使用 Not 和 Else 運算子  
>   
>      如需詳細資訊，請參閱 [商務規則範例](../master-data-services/business-rule-examples-master-data-services.md)。  
> -   實作自訂索引  
>   
>      如需詳細資訊，請參閱[自訂索引 &#40;Master Data Services&#41;](../master-data-services/custom-index-master-data-services.md)。  
 

 
 在 Master Data Services 中，套件是一個 XML 檔案，其中包含可部署的模型結構，以及模型中的資料 (選擇性)。 使用模型套件將模型的複本從一個 MDS 環境移到另一個 MDS 環境，或在現有的 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 環境中建立新的模型。  
  
## <a name="see-also"></a>另請參閱  
 [使用 MDSModelDeploy 部署模型部署套件](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)  
  
  
