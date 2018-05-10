---
title: 連接到 Azure Blob 儲存體 (SQL Server 匯入和匯出精靈) | Microsoft Docs
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: import-export-data
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e2e482b8-5f90-48c5-93fb-b412ed52659f
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 550e8323ef2a8997c72d28c58c4452097ed8ecc0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="connect-to-azure-blob-storage-sql-server-import-and-export-wizard"></a>連接到 Azure Blob 儲存體 (SQL Server 匯入和匯出精靈)
本主題示範如何透過 [SQL Server 匯入和匯出精靈] 的 [選擇資料來源] 或 [選擇目的地] 頁面，連接到 **Azure Blob 儲存體**資料來源。

>   [!NOTE]
> 若要使用 Azure Blob 來源或目的地，您必須安裝適用於 SQL Server Integration Services 的 Azure Feature Pack。
> - 若要下載此 Feature Pack，請參閱 [Microsoft SQL Server 2016 Integration Services Feature Pack for Azure](https://www.microsoft.com/download/details.aspx?id=49492)。
>
> - 如需詳細資訊，請參閱 [Azure Feature Pack for Integration Services &#40;SSIS&#41;](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)。

下列螢幕擷取畫面顯示連接到 Azure Blob 儲存體的設定選項。

![Azure blob 儲存體連接](../../integration-services/import-export-data/media/azure-blob-storage-connection.png)

## <a name="options-to-specify"></a>要指定的選項

> [!NOTE]
> 不論 Azure Blob 儲存體是您的來源還是目的地，此資料提供者的連接選項都會相同。 也就是，您在精靈的 [選擇資料來源] 和 [選擇目的地] 頁面上看到的選項會相同。

 **使用 Azure 帳戶**  
 指定是否要使用線上帳戶。
  
 **儲存體帳戶名稱**  
 輸入 Azure 儲存體帳戶的名稱。  
  
**帳戶金鑰**  
輸入 Azure 儲存體帳戶的金鑰。  
  
 **使用 HTTPS**  
 指定要使用 HTTP 或 HTTPS 連線到儲存體帳戶。  
  
 **使用本機開發人員帳戶**  
 指定是否在本機電腦上使用儲存體模擬器。  
  
 **Blob 容器名稱**  
 從指定儲存體帳戶的可用儲存體容器清單中選取。  
  
 **Blob 檔案格式**  
 選取 [文字] 或 [Avro] 檔案格式。  
  
 **資料行分隔符號字元**  
 如果您選取了 [文字] 格式，請輸入資料行分隔符號字元。  
  
 **使用第一個資料列作為資料行名稱**  
 指定資料的第一個資料列是否包含資料行名稱。  

## <a name="see-also"></a>另請參閱
[選擇資料來源](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[選擇目的地](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

