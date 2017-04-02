---
title: "封裝的重新部署 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "重新部署封裝 [Integration Services]"
  - "部署封裝 [Integration Services], 重新部署"
ms.assetid: 86806efb-8cf4-4f9d-9824-1152cb4c495c
caps.latest.revision: 37
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 37
---
# 封裝的重新部署
  在部署專案後，您可能需要更新或擴充封裝功能，然後部署包含已更新封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。 做為重新部署封裝處理的一部分，您應該檢視包含在部署公用程式中的組態屬性。 例如，您可能不允許組態在重新部署封裝之後變更。  
  
## 重新部署程序  
 在封裝更新完成後，您會重新建置專案、將部署資料夾複製到目標電腦，然後傳回 [封裝安裝精靈]。  
  
 如果您只更新專案中的幾個封裝，則可能不想重新部署整個專案。 若要只部署幾個封裝，您可以建立新的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案、將已更新的封裝加入新的專案，然後建立和部署該專案。 當您將封裝加入其他專案時，封裝組態會自動隨封裝一同複製。  
  
## 相關工作  
 [使用部署公用程式來部署封裝](../../integration-services/packages/deploy-packages-by-using-the-deployment-utility.md)  
  
  