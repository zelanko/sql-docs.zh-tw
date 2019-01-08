---
title: 監視封裝執行和其他作業 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: cbbcd79f-ab9b-46ec-84cb-4821c1d16b99
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: eb705b82ec9f03de8cc458e62eded9f1817850c0
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53356779"
---
# <a name="monitoring-for-package-executions-and-other-operations"></a>監視封裝執行和其他作業
  您可以使用下列其中一項或多項工具，監視 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 執行封裝、專案驗證及其他作業。 某些工具 (例如資料點選) 僅適用於部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器的專案。  
  
-   記錄檔  
  
     如需詳細資訊，請參閱 [集成服務 &#40;SSIS&#41; 記錄](integration-services-ssis-logging.md)。  
  
-   報表  
  
     如需詳細資訊，請參閱 [Reports for the Integration Services Server](../reports-for-the-integration-services-server.md)。  
  
-   檢視  
  
     如需詳細資訊，請參閱[檢視 &#40;Integration Services 目錄&#41;](/sql/integration-services/system-views/views-integration-services-catalog)。  
  
-   效能計數器  
  
     如需相關資訊，請參閱 [Performance Counters](performance-counters.md)。  
  
-   資料點選  
  
## <a name="operation-types"></a>作業類型  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器上的 `SSISDB` 目錄中會監視數個不同類型的作業。 每個作業都可以有多則與其相關聯的訊息。 每則訊息可以分類在數種不同的類型之一。 例如，訊息可以是資訊、警告或錯誤等類型。 如需訊息類型的完整清單，請參閱 Transact-SQL [catalog.operation_messages &#40;SSISDB Database&#41;](/sql/integration-services/system-views/catalog-operation-messages-ssisdb-database) 檢視的文件集。 如需作業類型的完整清單，請參閱 [catalog.operations &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-views/catalog-operations-ssisdb-database)。  
  
 有九種不同的狀態類型可用來指示作業的狀態。 如需狀態類型的完整清單，請參閱 [catalog.operations &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-views/catalog-operations-ssisdb-database) 檢視。  
  
## <a name="related-content"></a>相關內容  
 blogs.msdn.com 上的部落格文章： [SSIS T-SQL API Overview](https://go.microsoft.com/fwlink/?LinkId=249051)(SSIS T-SQL API 概觀)。  
  
  
