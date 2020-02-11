---
title: Integration Services 服務 (SSIS 服務) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services service, about Integration Services service
- SQL Server Integration Services service
- service [Integration Services],about Integration Services service
- service [Integration Services]
- SQL Server Integration Services, service
ms.assetid: 2c785b3b-4a0c-4df7-b5cd-23756dc87842
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7eb8f74e271b9d5c19cedab4fd25069eb5a0e2b1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62766680"
---
# <a name="integration-services-service-ssis-service"></a>Integration Services 服務 (SSIS 服務)
  本節中的主題討論 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務 (用於管理 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝的 Windows 服務)。 若要建立、儲存及執行 Integration Services 封裝，則不需要這項服務。 
  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 支援 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務能與舊版 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]回溯相容。  
  
 從開始[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]會針對使用專案部署模型部署至`SSISDB` [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]伺服器的專案，將物件、設定和運算元據儲存在資料庫中。 
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器是主控資料庫之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Database Engine 的執行個體。 如需資料庫的詳細資訊，請參閱 [SSIS 目錄](../catalog/ssis-catalog.md)。 如需將專案部署至 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器的詳細資訊，請參閱 [將專案部署至 Integration Services 伺服器](../deploy-projects-to-integration-services-server.md)。  
  
## <a name="management-capabilities"></a>管理功能  
 
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務是可用於管理 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝的 Windows 服務。 
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務只可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中使用。  
  
 執行 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務會提供下列管理功能：  
  
-   啟動遠端和本機儲存的封裝  
  
-   停止遠端和本機正在執行的封裝  
  
-   監視遠端和本機正在執行的封裝  
  
-   匯入和匯出封裝  
  
-   管理封裝儲存體  
  
-   自訂儲存資料夾  
  
-   服務停止時停止正在執行的封裝  
  
-   檢視 Windows 事件記錄檔  
  
-   連接多個 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器  
  
## <a name="startup-type-for-integration-services-service"></a>Integration Services 服務的啟動類型  
 當安裝 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 元件時，會安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服務。 根據預設， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務會啟動，而且服務的啟動類型會設為自動。 該服務必須執行，才能監視儲存在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝存放區」中的封裝。 
  [!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝存放區可以是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中的 msdb 資料庫，也可以是檔案系統中的指定資料夾。  
  
 如果只想設計和執行 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝，則無需執行 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務。 不過，若要使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]列出和監視封裝，則需要該服務。  
  
## <a name="related-tasks"></a>相關工作  
  
-   [設定 Integration Services 服務的屬性](../set-the-properties-of-the-integration-services-service.md)  
  
-   [檢視 Integration Services 服務的事件](../view-events-for-the-integration-services-service.md)  
  
  
