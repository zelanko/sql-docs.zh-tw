---
title: Microsoft Connector for SAP BW | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5281f080-53d5-4679-aa26-f4cd4ac7a2df
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 12375a5d09c34ac9b9e79e99efdee3ccebbe823b
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86918092"
---
# <a name="microsoft-connector-for-sap-bw"></a>Microsoft Connector for SAP BW

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


  [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW 包含了三個為一組的元件，可讓您擷取 SAP Netweaver BW 版本 7 系統中的資料，或是將資料載入至該系統。  
  
 適用於 SQL Server 2016 的 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW 是 SQL Server 2016 Feature Pack 的元件。 若要安裝 Connector for SAP BW 及其文件，請從 [SQL Server 2016 Feature Pack 網頁](https://go.microsoft.com/fwlink/?LinkId=746297)下載並執行安裝程式。  

> [!IMPORTANT]
> Microsoft 不打算提供更新版本的 Connector for SAP BW。 Microsoft 並未擁有 SAP BW 元件的原始程式碼，它是由協力廠商所開發，因此無法更新。 請考慮從 Microsoft ISV 夥伴，例如 [Theobald Software](https://theobald-software.com/en/xtract-is-productinfo.html)，購買最新的 SAP 連線元件。 Microsoft 的 ISV 夥伴針對 SSIS 已調整其 SAP 連線元件，以便在 Azure 中安裝。
 
> [!IMPORTANT]  
>  Microsoft Connector for SAP BW 的文件假設使用者已熟悉 SAP Netweaver BW 環境。 如需有關 SAP Netweaver BW 的詳細資訊，或有關如何設定 SAP Netweaver BW 物件與處理序的詳細資訊，請參閱 SAP 文件集。  
  
> [!IMPORTANT]  
>  擷取 SAP Netweaver BW 中的資料需要額外的 SAP 授權。 請洽詢 SAP 以確認這些需求。  
  
## <a name="components"></a>元件  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW 具有下列元件：  
  
-   **SAP BW 來源** - SAP BW 來源是一個資料流程來源元件，可讓您擷取 SAP Netweaver BW 版本 7 系統中的資料。  
  
-   **SAP BW 目的地** - SAP BW 目的地是一個資料流程目的地元件，可讓您將資料載入至 SAP Netweaver BW 版本 7 系統中。  
  
-   **SAP BW 連線管理員** - SAP BW 連線管理員可將 SAP BW 來源或 SAP BW 目的地連接至 SAP Netweaver BW 版本 7 系統。  
  
 如需示範如何設定及使用 SAP BW 連線管理員、來源和目的地的逐步解說，請參閱技術白皮書： [Using SQL Server Integration Services with SAP BI 7.0](https://go.microsoft.com/fwlink/?LinkId=301897)(搭配 SAP BI 7.0 使用 SQL Server Integration Services)。 這份技術白皮書也會示範如何設定 SAP BW 中的必要物件。  
  
## <a name="documentation"></a>文件  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW 的這個說明檔包含以下主題和章節：  
  
 [安裝 Microsoft Connector for SAP BW](../integration-services/installing-the-microsoft-connector-for-sap-bw.md)  
 說明 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW 的安裝需求。  
  
 [Microsoft Connector for SAP BW 元件](../integration-services/microsoft-connector-for-sap-bw-components.md)  
 說明 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW 的每一個元件。  
  
 [Microsoft Connector for SAP BW F1 說明](../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
 說明 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW 中每一個元件的使用者介面。  
  
  
