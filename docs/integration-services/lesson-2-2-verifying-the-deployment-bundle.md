---
description: 課程 2-2 - 確認部署配套
title: 步驟 2:確認部署配套 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 6c13f5c9-c75e-4e52-94dc-2d2db2c578fe
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4704aea54f73a0fa25db60ab9145a0ad3bc9359d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449662"
---
# <a name="lesson-2-2---verifying-the-deployment-bundle"></a>課程 2-2 - 確認部署配套

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


在第 1 課中，您建立了「部署教學課程」專案，並且將封裝和輔助檔案加入至專案中。在上一項工作中，您為專案建立了部署公用程式。  
  
在這項工作中，您會確認部署配套的內容。 部署配套就是您將要複製到目的地電腦上並且用來安裝封裝的資料夾。 如果您使用預設值 (bin\Deployment) 作為部署公用程式的位置，則部署配套就是 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案中 [部署教學課程] 資料夾內的 Bin\Deployment 資料夾。  
  
### <a name="to-verify-the-content-of-deployment-bundle"></a>若要確認部署配套的內容  
  
1.  在電腦上找到 bin\Deployment 資料夾。  
  
2.  確認下列檔案存在：  
  
    -   DataTransfer.dtsx  
  
    -   datatransferconfig.dtsconfig  
  
    -   Deployment Tutorial.SSISDeploymentManifest  
  
    -   LoadXMLData.dtsx  
  
    -   loadxmldataconfig.dtsconfig  
  
    -   NewCustomers.txt  
  
    -   orders.xml  
  
    -   orders.xsd  
  
    -   Readme.txt  
  
3.  以滑鼠右鍵按一下 Deployment Tutorial.SSISDeploymentManifest，並指向 [開啟方式]  ，然後按一下 [Internet Explorer]  。 您也可以在「記事本」之類的文字編輯器中開啟此檔案。 此檔案的 XML 程式碼應該如下所示：  
  
    `<?xml version="1.0"?><DTSDeploymentManifest GeneratedBy="Domain\UserName" GeneratedFromProjectName="Deployment Tutorial" GeneratedDate="2006-02-24T13:29:02.6537669-08:00" AllowConfigurationChanges="true"><Package>DataTransfer.dtsx</Package><Package>LoadXMLData.dtsx</Package><ConfigurationFile>datatransferconfig.dtsconfig</ConfigurationFile><ConfigurationFile>loadxmldataconfig.dtsconfig</ConfigurationFile><MiscellaneousFile>Readme.txt</MiscellaneousFile><MiscellaneousFile>orders.xml</MiscellaneousFile><MiscellaneousFile>NewCustomers.txt</MiscellaneousFile><MiscellaneousFile>orders.xsd</MiscellaneousFile></DTSDeploymentManifest>`  
  
4.  確認 **AllowConfigurationChanges** 屬性的值為 **true** ，而且 XML 中的兩個套件都各包含 **Package** 元素，四個非套件檔案都各包含 **MiscellaneousFile** 元素，以及兩個 XML 組態檔都各包含 **ConfigurationFile** 元素。  
  
5.  結束 Internet Explorer 或文字編輯器。  
  
## <a name="next-lesson"></a>下一課  
[第 3 課：安裝 SSIS 套件](../integration-services/lesson-3-install-ssis-packages.md)  
  
  
  
