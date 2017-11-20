---
title: "SQL Server Integration Services (SSIS) 向外的延展 |Microsoft 文件"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: dcfbd1c5-c001-4fb7-b9ae-916e49ab6a96
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: ce7fb96901e8af4da74392fe0a0a85c6e2ec05a4
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="integration-services-ssis-scale-out"></a>Integration Services (SSIS) 相應放大
[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 相應放大透過將執行分散到多部電腦，來提供高效能套件執行。 您可以送出多個 SQL Server Management Studio 中的封裝執行的要求。 這些套件將會以相應放大模式平行執行。  

[!INCLUDE[ssIS_md](../../includes/ssis-md.md)]向外組成[!INCLUDE[ssIS_md](../../includes/ssis-md.md)]標尺出主要和一個或多個[!INCLUDE[ssIS_md](../../includes/ssis-md.md)]標尺出背景工作。 相應放大主機負責相應放大管理，以及接收來自使用者的套件執行要求。 相應放大背景工作會從相應放大主機提取執行工作，並執行套件執行工作。 如需詳細資訊，請參閱[相應放大主機](integration-services-ssis-scale-out-master.md)和[相應放大背景工作](integration-services-ssis-scale-out-worker.md)。

[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]向外可以設定一個在電腦上，在其中一個標尺出主要和標尺出背景工作會設定在電腦上並存。 相應放大也可以在多部電腦上執行，其中，每個相應放大背景工作都是位在不同的電腦上。
- [逐步解說：設定 Integration Services 相應放大](walkthrough-set-up-integration-services-scale-out.md)

相應放大支援在 SSISDB 目錄中平行執行多個套件。 如需詳細資訊，請參閱[在相應放大中執行套件](run-packages-in-integration-services-ssis-scale-out.md)。

