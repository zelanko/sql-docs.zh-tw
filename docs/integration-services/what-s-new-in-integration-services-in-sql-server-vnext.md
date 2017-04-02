---
title: "SQL Server vNext Integration Services 的新功能 | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e26d7884-e772-46fa-bfdc-38567fe976a1
caps.latest.revision: 4
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 3
---
# SQL Server vNext Integration Services 的新功能
本主題說明 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中已新增或更新的功能。

>   [!NOTE] SQL Server vNext 也包含 SQL Server 2016 的功能以及 SQL Server 2016 更新中加入的功能。 如需 SQL Server 2016 的 SSIS 新功能資訊，請參閱 [SQL Server 2016 的 Integration Services 新功能](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)。

## <a name="new-in-ssis-in-sql-server-vnext-ctp-11"></a>SQL Server vNext CTP 1.1 的 SSIS 新功能

SQL Server vNext CTP 1.1 中沒有任何 SSIS 新功能。

## <a name="new-in-ssis-in-sql-server-vnext-ctp-10"></a>SQL Server vNext CTP 1.0 的 SSIS 新功能

### <a name="scale-out-for-ssis"></a>SSIS 相應放大

相應放大功能讓 [!INCLUDE[ssIS_md](../includes/ssis-md.md)] 更容易在多部電腦上執行。 
   
安裝相應放大主機和背景工作之後，封裝即可發佈到不同的背景工作自動執行。 如果執行意外終止，它會自動重試。 而且，所有執行和背景工作都可以使用主機集中管理。
   
如需詳細資訊，請參閱 [Integration Services 相應放大](../integration-services/integration-services-ssis-scale-out.md)。
   
### <a name="support-for-microsoft-dynamics-online-resources"></a>Microsoft Dynamics Online 資源的支援

OData 來源和 OData 連接管理員現在支援連接到 Microsoft Dynamics AX Online 和 Microsoft Dynamics CRM Online 的 OData 摘要。
