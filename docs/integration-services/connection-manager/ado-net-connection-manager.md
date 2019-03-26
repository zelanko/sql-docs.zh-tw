---
title: ADO.NET 連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.adonetconnection.f1
helpviewer_keywords:
- connection managers [Integration Services], ADO.NET
- ADO.NET connection manager [Integration Services]
- connections [Integration Services], ADO.NET
ms.assetid: fc5daa2f-0159-4bda-9402-c87f1035a96f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d5811c4ea89a177f9862f27ba75f6baaddef7208
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/20/2019
ms.locfileid: "58272376"
---
# <a name="adonet-connection-manager"></a>ADO.NET 連接管理員
  [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連接管理員可讓封裝使用 .NET 提供者來存取資料來源。 此連線管理員通常用於存取 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]這類的資料來源，以及透過自訂工作 (使用如 C# 這類語言以 Managed 程式碼撰寫) 中之 OLE DB 和 XML 公開的資料來源。  
  
 當您將 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連線管理員加入封裝時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會建立一個連線管理員 (在執行階段會解析為 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連接)、設定連線管理員屬性，並將該連線管理員加入封裝上的 **Connections** 集合。  
  
 連線管理員的 **ConnectionManagerType** 屬性會設為 **ADO.NET**。 系統會限定 **ConnectionManagerType** 的值，以包含連線管理員使用之 .NET 提供者的名稱。  
  
## <a name="adonet-connection-manager-troubleshooting"></a>ADO.NET 連接管理員疑難排解  
 您可以記錄 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連接管理員對外部資料提供者執行的呼叫。 您可以使用這項記錄功能，疑難排解 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連接管理員對外部資料來源執行的連接。 若要記錄 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連線管理員對外部資料提供者執行的呼叫，請啟用封裝記錄，然後在封裝層級選取 [診斷] 事件。 如需詳細資訊，請參閱 [封裝執行的疑難排解工具](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)。  
  
 由 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連線管理員讀取時，某些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 日期資料類型的資料將會產生如下表所示的結果。  
  
|SQL Server 資料類型|結果|  
|--------------------------|------------|  
|**time**, **datetimeoffset**|除非封裝使用參數化 SQL 命令，否則封裝會失敗。 若要使用參數化 SQL 命令，請在封裝中使用「執行 SQL 工作」。 如需詳細資訊，請參閱 [執行 SQL 工作](../../integration-services/control-flow/execute-sql-task.md) 和 [執行 SQL 工作中的參數和傳回碼](https://msdn.microsoft.com/library/a3ca65e8-65cf-4272-9a81-765a706b8663)。|  
|**datetime2**|[!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連接管理員會截斷毫秒值。|  
  
> [!NOTE]  
>  如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型以及如何將其對應到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 資料類型的詳細資訊，請參閱[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md) 和 [Integration Services 資料類型](../../integration-services/data-flow/integration-services-data-types.md)。  
  
## <a name="adonet-connection-manager-configuration"></a>ADO.NET 連接管理員組態  
 您可以利用下列方式設定 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連線管理員：  
  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
-   提供設定的特定連接字串，以符合所選 .NET 提供者的需求。  
  
-   視提供者而定，包含要連接的資料來源名稱。  
  
-   為所選的提供者提供適當的安全性認證。  
  
-   指示是否在執行階段保留從連接管理員建立的連接。  
  
 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連線管理員的許多組態選項依存於連線管理員使用的 .NET 提供者。  
  
 如需可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [設定 ADO.NET 連接管理員](../../integration-services/connection-manager/configure-ado-net-connection-manager.md)  
  
 如需以程式設計方式設定連線管理員的資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和 [以程式設計方式加入連接](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)。  
  
## <a name="configure-adonet-connection-manager"></a>設定 ADO.NET 連接管理員
  使用 [設定 ADO.NET 連線管理員] 對話方塊加入資料來源的連接，可使用 .NET Framework 資料提供者 (例如 SqlClient 提供者) 來存取此資料來源。 連接管理員可以使用現有的連接，或者您也可以建立新的連接。  
  
 若要深入了解 ADO.NET 連線管理員，請參閱 [ADO.NET 連線管理員](../../integration-services/connection-manager/ado-net-connection-manager.md)。  
  
### <a name="options"></a>選項。  
 **資料連接**  
 從清單中選取現有的 ADO.NET 資料連接。  
  
 **資料連接屬性**  
 檢視選取之 ADO.NET 資料連接的屬性和值。  
  
 **新增**  
 使用 [連線管理員] 對話方塊來建立 ADO.NET 資料連接。  
  
 **刪除**  
 請選取一個連接，然後使用 [刪除] 按鈕刪除它。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41; 連接](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  
