---
title: ADO.NET 連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connection managers [Integration Services], ADO.NET
- ADO.NET connection manager [Integration Services]
- connections [Integration Services], ADO.NET
ms.assetid: fc5daa2f-0159-4bda-9402-c87f1035a96f
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 850c8f0f54339594b19debd48ebf4ac7021873d3
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84921226"
---
# <a name="adonet-connection-manager"></a>ADO.NET 連接管理員
  [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連接管理員可讓封裝使用 .NET 提供者來存取資料來源。 此連線管理員通常用於存取資料來源（例如 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ），以及透過使用 c # 這類語言以 managed 程式碼撰寫之自訂工作中的 OLE DB 和 XML 公開的資料來源。  
  
 當您將 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連線管理員加入封裝時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會建立在執行時間解析為連接的連線管理員 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 、設定連線管理員屬性，並將連線管理員加入 `Connections` 封裝上的集合。  
  
 連接管理員的 `ConnectionManagerType` 屬性會設為 `ADO.NET`。 系統會限定 `ConnectionManagerType` 的值，以包含連接管理員使用之 .NET 提供者的名稱。  
  
## <a name="adonet-connection-manager-troubleshooting"></a>ADO.NET 連接管理員疑難排解  
 您可以記錄 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連接管理員對外部資料提供者執行的呼叫。 您可以使用這項記錄功能，疑難排解 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連接管理員對外部資料來源執行的連接。 若要記錄 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連線管理員對外部資料提供者執行的呼叫，請啟用封裝記錄，然後在封裝層級選取 [診斷]**** 事件。 如需詳細資訊，請參閱 [封裝執行的疑難排解工具](../troubleshooting/troubleshooting-tools-for-package-execution.md)。  
  
 由 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連線管理員讀取時，某些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 日期資料類型的資料將會產生如下表所示的結果。  
  
|SQL Server 資料類型|結果|  
|--------------------------|------------|  
|`time`, `datetimeoffset`|除非封裝使用參數化 SQL 命令，否則封裝會失敗。 若要使用參數化 SQL 命令，請在封裝中使用「執行 SQL 工作」。 如需詳細資訊，請參閱 [執行 SQL 工作](../control-flow/execute-sql-task.md) 和 [執行 SQL 工作中的參數和傳回碼](../parameters-and-return-codes-in-the-execute-sql-task.md)。|  
|`datetime2`|[!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連接管理員會截斷毫秒值。|  
  
> [!NOTE]  
>  如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型以及如何將其對應到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 資料類型的詳細資訊，請參閱[資料類型 &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql) 和 [Integration Services 資料類型](../data-flow/integration-services-data-types.md)。  
  
## <a name="adonet-connection-manager-configuration"></a>ADO.NET 連接管理員組態  
 您可以利用下列方式設定 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連線管理員：  
  
 您可以透過 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
-   提供設定的特定連接字串，以符合所選 .NET 提供者的需求。  
  
-   視提供者而定，包含要連接的資料來源名稱。  
  
-   為所選的提供者提供適當的安全性認證。  
  
-   指示是否在執行階段保留從連接管理員建立的連接。  
  
 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連線管理員的許多組態選項依存於連線管理員使用的 .NET 提供者。  
  
 如需可在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [設定 ADO.NET 連接管理員](../configure-ado-net-connection-manager.md)  
  
 如需以程式設計方式設定連線管理員的資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和 [以程式設計方式加入連接](../building-packages-programmatically/adding-connections-programmatically.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41; 連接](integration-services-ssis-connections.md)  
  
  
