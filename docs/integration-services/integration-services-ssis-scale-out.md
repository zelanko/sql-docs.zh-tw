---
title: "Integration Services (SSIS) 相應放大 | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: dcfbd1c5-c001-4fb7-b9ae-916e49ab6a96
caps.latest.revision: 6
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 6
---
# Integration Services (SSIS) 相應放大
[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 相應放大透過將執行分散到多部電腦，來提供高效能套件執行。 您可以在 SQL Server Management Studio 中提交多個套件執行的要求。 這些套件將會以相應放大模式平行執行。  


## <a name="ssis-scale-out-master-and-scale-out-worker"></a>SSIS 相應放大主機和相應放大背景工作
[!INCLUDE[ssIS_md](../includes/ssis-md.md)] 相應放大包含一個 [!INCLUDE[ssIS_md](../includes/ssis-md.md)] 相應放大主機和數個 [!INCLUDE[ssIS_md](../includes/ssis-md.md)] 相應放大背景工作。 相應放大主機負責相應放大管理，以及接收來自使用者的套件執行要求。 相應放大背景工作會從相應放大主機提取執行工作，並執行套件執行工作。 如需詳細資訊，請參閱[相應放大主機](../integration-services/integration-services-ssis-scale-out-master.md)和[相應放大背景工作](../integration-services/integration-services-ssis-scale-out-worker.md)。


## <a name="how-to-set-up-scale-out"></a>如何設定相應放大
[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 相應放大可以在一部電腦上執行，而電腦上同時設定相應放大主機和相應放大背景工作。 相應放大也可以在多部電腦上執行，其中，每個相應放大背景工作都是位在不同的電腦上。
- [逐步解說：設定 Integration Services 相應放大](../integration-services/walkthrough-set-up-integration-services-scale-out.md)


## <a name="run-packages-in-scale-out"></a>在相應放大中執行套件
相應放大支援在 SSISDB 目錄中平行執行多個套件。 如需詳細資訊，請參閱[在相應放大中執行套件](../integration-services/run-packages-in-integration-services-ssis-scale-out.md)。

