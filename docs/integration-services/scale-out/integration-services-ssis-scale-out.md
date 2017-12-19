---
title: SQL Server Integration Services (SSIS) Scale Out | Microsoft Docs
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: dcfbd1c5-c001-4fb7-b9ae-916e49ab6a96
caps.latest.revision: "6"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 0277d312ce4dab14e7ba64529e3eb2251a0d2d02
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="integration-services-ssis-scale-out"></a>Integration Services (SSIS) 相應放大
[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 相應放大透過將執行分散到多部電腦，來提供高效能套件執行。 您可以在 SQL Server Management Studio 中提交多個套件執行的要求。 這些套件將會以相應放大模式平行執行。  

[!INCLUDE[ssIS_md](../../includes/ssis-md.md)] Scale Out 包含一部 [!INCLUDE[ssIS_md](../../includes/ssis-md.md)] Scale Out 主機及一或多個 [!INCLUDE[ssIS_md](../../includes/ssis-md.md)] Scale Out 背景工作角色。 相應放大主機負責相應放大管理，以及接收來自使用者的套件執行要求。 相應放大背景工作會從相應放大主機提取執行工作，並執行套件執行工作。 如需詳細資訊，請參閱[相應放大主機](integration-services-ssis-scale-out-master.md)和[相應放大背景工作](integration-services-ssis-scale-out-worker.md)。

[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out 可以在一部電腦上設定，而電腦上同時設定 Scale Out 主機和 Scale Out背景工作角色。 相應放大也可以在多部電腦上執行，其中，每個相應放大背景工作都是位在不同的電腦上。
- [逐步解說：設定 Integration Services 相應放大](walkthrough-set-up-integration-services-scale-out.md)

相應放大支援在 SSISDB 目錄中平行執行多個套件。 如需詳細資訊，請參閱[在相應放大中執行套件](run-packages-in-integration-services-ssis-scale-out.md)。
