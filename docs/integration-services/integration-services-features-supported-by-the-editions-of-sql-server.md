---
title: "Integration Services 的 SQL Server 版本所支援的功能 |Microsoft 文件"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e5018225-68bb-4f34-ae4a-ead79d8ad13a
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 8cc1fcfdeae8742a93916dfb08c9db1215f88721
ms.openlocfilehash: e9d1b8851f113fa44264230a79d0e496007ed96b
ms.contentlocale: zh-tw
ms.lasthandoff: 10/17/2017

---
# <a name="integration-services-features-supported-by-the-editions-of-sql-server"></a>SQL server 版本所支援的 integration Services 功能
 本主題提供不同 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)]版本所支援之 SQL Server Integration Services (SSIS) 功能的詳細資訊。  

如需 Evaluation 和 Developer edition 所支援的功能，請參閱下表列出適用於 Enterprise Edition 的功能。
  
最新的版本資訊和什麼是新的資訊，請參閱下列文章：
-   [SQL Server 2016 版本資訊](../sql-server/sql-server-2016-release-notes.md)
-   [SQL Server 2016 Integration Services 的新功能](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)
-   [SQL Server 2017 中的 Integration Services 新增功能](../integration-services/what-s-new-in-integration-services-in-sql-server-2017.md)
    
**試用 SQL Server 2016！**    

SQL Server Evaluation Edition 提供了 180 天的試用期。  
    
> [![從 Evaluation Center 下載](../analysis-services/media/download.png)](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) **[從 Evaluation Center 下載 SQL Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**    
    
## <a name="ISNew"></a>SQL Server 2017 中新的 Integration Services 功能
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|向外延展 Master|是|||||
|向外延展背景工作|是|是 <sup>1</sup>|TBD|TBD|TBD|
|支援 OData 元件中的 Microsoft Dynamics AX 和 Microsoft Dynamics CRM <sup>2</sup>|是|是||||

<sup>1</sup>標尺出工作者如果您執行封裝所需的企業專用的功能，在向外，也必須在 SQL Server enterprise 的執行個體上執行。

<sup>2</sup>含 Service Pack 1 的 SQL Server 2016 中也會支援這項功能。

## <a name="IEWiz"></a>SQL Server 匯入和匯出精靈

|功能|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|SQL Server 匯入和匯出精靈|是|是|是|是|是|  

## <a name="IS"></a> Integration Services  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|內建的資料來源連接器|是|是|||| 
|內建工作和轉換|是|是||||  
|ODBC 來源和 by Attunity 的目的地|是|是|||| 
|Azure 資料來源連接器和工作|是|是||||  
|Hadoop/HDFS 連接器和工作|是|是||||  
|基本資料分析工具|是|是|||| 

## <a name="ISAA"></a>Integration Services-進階來源和目的地  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|高效能 Oracle 來源和 by Attunity 的目的地|是|||||  
|高效能 Teradata 來源和 by Attunity 的目的地|是|||||  
|SAP BW 來源和目的地|是|||||  
|資料採礦模型定型目的地|是|||||  
|維度處理目的地|是|||||  
|資料分割處理目的地|是|||||  
  
## <a name="ISAT"></a>Integration Services-進階工作和轉換  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|異動資料擷取元件 by Attunity <sup>1</sup>|是|||||  
|資料採礦查詢轉換|是|||||  
|模糊群組 」 和 「 模糊查閱轉換|是|||||  
|詞彙擷取 」 和 「 詞彙查閱轉換|是|||||  

<sup>1</sup> by Attunity 異動資料擷取的元件需要 Enterprise edition。 Change Data Capture Service 和 Change Data Capture Designer，不過，不需要企業版。 您可以使用設計工具和服務的電腦上未安裝 SSIS。

