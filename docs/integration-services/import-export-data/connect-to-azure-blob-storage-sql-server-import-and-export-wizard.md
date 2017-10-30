---
title: "連接到 Azure Blob 儲存體 （SQL Server 匯入和匯出精靈） |Microsoft 文件"
ms.custom: 
ms.date: 02/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e2e482b8-5f90-48c5-93fb-b412ed52659f
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 36b992b5141799d4e168b2e990643e6a515a8d69
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="connect-to-azure-blob-storage-sql-server-import-and-export-wizard"></a>連接到 Azure Blob 儲存體 （SQL Server 匯入和匯出精靈）
本主題說明如何連接到**Azure Blob 儲存體**資料來源從**選擇資料來源**或**選擇目的地**SQL Server 匯入和匯出精靈 頁面。

>   [!NOTE]
> 若要使用 Azure Blob 來源或目的地，您必須安裝 Azure Feature Pack for SQL Server Integration Services。
> - 若要下載 Feature Pack，請參閱[Microsoft SQL Server 2016 Integration Services 功能套件 azure](https://www.microsoft.com/download/details.aspx?id=49492)。
>
> - 如需詳細資訊，請參閱 [Azure Feature Pack for Integration Services &#40;SSIS&#41;](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)。

下列螢幕擷取畫面顯示，以連接至 Azure Blob 儲存體設定的選項。

![Azure blob 儲存體連接](../../integration-services/import-export-data/media/azure-blob-storage-connection.png)

## <a name="options-to-specify"></a>若要指定的選項

> [!NOTE]
> Azure Blob 儲存體是您的來源或目的地連接選項，此資料提供者都是相同的。 也就是您所看到的選項會同時針對相同**選擇資料來源**和**選擇目的地**精靈頁面。

 **使用 Azure 帳戶**  
 指定是否要使用線上帳戶。
  
 **儲存體帳戶名稱**  
 輸入 Azure 儲存體帳戶名稱。  
  
**帳戶金鑰**  
輸入 Azure 儲存體帳戶金鑰。  
  
 **使用 HTTPS**  
 指定要使用 HTTP 或 HTTPS 連線到儲存體帳戶。  
  
 **使用本機開發人員帳戶**  
 指定是否在本機電腦上使用儲存體模擬器。  
  
 **Blob 容器名稱**  
 從指定儲存體帳戶的可用儲存體容器清單中選取。  
  
 **Blob 檔案格式**  
 選取 [文字] 或 [Avro] 檔案格式。  
  
 **資料行分隔符號字元**  
 如果您選取文字格式，輸入資料行分隔符號字元。  
  
 **使用第一個資料列作為資料行名稱**  
 指定資料的第一個資料列是否包含資料行名稱。  

## <a name="see-also"></a>另請參閱
[選擇資料來源](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[選擇目的地](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


