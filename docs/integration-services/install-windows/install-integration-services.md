---
title: 安裝 SQL Server Integration Services (SSIS) | Microsoft Docs
description: 了解如何安裝 Microsoft SQL Server Integration Services (SSIS)，以及如何取得適用於 SSIS 的其他下載
ms.custom: ''
ms.date: 07/03/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services, installing
- SSIS, installing
- installing Integration Services, about installing Integration Services
- SQL Server Integration Services, installing
- Setup [Integration Services], about installing Integration Services
- installing Integration Services
- Setup [Integration Services]
ms.assetid: bd20fd3a-414b-4581-959d-ebba4ddf5a55
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8d1ef66f97683b24014661fb6a1e633ce6ce06ce
ms.sourcegitcommit: 96032813f6bf1cba680b5e46d82ae1f0f2da3d11
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/15/2019
ms.locfileid: "54299915"
---
# <a name="install-integration-services"></a>安裝 Integration Services

  > [!div class="nextstepaction"]
  > [請提供您對 SQL Docs 目錄的意見反應！](https://aka.ms/sqldocsurvey)

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供了單一安裝程式，以安裝它的任何或所有元件，包含 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]在內。 使用安裝程式來安裝 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]，不論單一電腦上是否有其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件。    
    
 本文特別介紹在您安裝 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 之前應該先了解的重要考量事項。 本文的資訊有助您評估安裝選項，以便做出讓安裝成功的選擇。    
    
## <a name="get-ready-to-install-integration-services"></a>準備好安裝 Integration Services    
 在安裝 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 之前，請檢閱下列資訊：    
    
-   [安裝 SQL Server 的硬體與軟體需求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)    
    
-   [SQL Server 安裝的安全性考量](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)    
    
## <a name="install-standalone-or-side-by-side"></a>獨立或並存安裝    
您可以在以下組態中安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ：    
    
-   您可以將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 安裝在沒有舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的電腦上。    
    
-   您可以將 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 與 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的現有執行個體並存安裝。    
    
當您為已安裝較早版本 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的電腦升級至最新版 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 時，目前版本會與舊版並存。    
    
如需升級 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的詳細資訊，請參閱[升級 Integration Services](../../integration-services/install-windows/upgrade-integration-services.md)。

## <a name="get-sql-server-with-integration-services"></a>取得隨附 Integration Services 的 SQL Server

如果您還沒有 Microsoft SQL Server，請下載 [SQL Server 下載](https://www.microsoft.com/sql-server/sql-server-downloads)免費的 Evaluation Edition 或免費的 Developer Edition。 SQL Server Express 版並未隨附 SSIS。

## <a name="install-integration-services"></a>安裝 Integration Services    
 在檢閱 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的安裝需求並確認電腦符合這些需求之後，您就可以開始安裝 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]。    
     
使用 [安裝精靈] 安裝 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 時，您會使用一連串的頁面來指定元件和選項。

-   在 [功能選取] 頁面中，選取 [共用功能] 底下的 **Integration Services**。

-   在 [執行個體功能] 下方，選擇性選取 **Database Engine Services** 來裝載 SSIS 目錄資料庫 (`SSISDB`)，以便儲存、管理、執行與監視 SSIS 套件。

-   若要安裝用於 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 程式設計的受控組件，另請選取 [共用功能] 下方的 [用戶端工具 SDK]。

> [!NOTE]
> [安裝精靈] 的 [功能選取] 頁面上提供一些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件供您選取安裝，以安裝 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的部分元件。 這些元件適用於特定的工作，但 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的功能有限。 例如，[Database Engine Services] 選項會安裝 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈] 所需的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 元件。 為了確保 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 能完整安裝，您必須在 [功能選擇] 頁面上選取 [Integration Services]。

### <a name="installing-a-dedicated-server-for-etl-processes"></a>安裝 ETL 的專用伺服器程序

若要使用專用伺服器進行擷取、轉換和載入 (ETL) 程序，請在安裝 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 時安裝 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的本機執行個體。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 通常會將封裝儲存在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體中，而且它會仰賴 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 來排程這些封裝。 如果 ETL 伺服器沒有 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體，您就必須從具有 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體的伺服器排程或執行套件。 這樣一來，套件就不是在 ETL 伺服器上執行，而會在啟動套件的伺服器上執行。 因此，系統將無法如預期方式使用專用 ETL 伺服器的資源。 此外，其他伺服器的資源可能會受到執行中 ETL 處理序的限制。

### <a name="configuring-ssis-event-logging"></a>設定 SSIS 事件記錄
    
根據預設，在新的安裝中， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會設定為不要將與封裝執行相關的事件記錄至應用程式事件記錄檔。 當您使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的資料收集器功能時，這個設定可避免產生過多的事件記錄項目。 不會記錄的事件包括 EventID 12288「封裝已啟動」和 EventID 12289「封裝已成功完成」。 若要將這些事件記錄到應用程式事件記錄檔，請開啟登錄進行編輯。 在登錄中找出 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\SSIS 節點，然後將 LogPackageExecutionToEventLog 設定的 DWORD 值從 0 變更為 1。    
    
## <a name="install-additional-components-for-integration-services"></a>安裝 Integration Services 的其他元件

若要進行 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的完整安裝，請從下列清單中選取您需要的元件：

-   **Integration Services (SSIS)**： 使用 [SQL Server 安裝精靈] 來安裝 SSIS。 選取 SSIS 時，會安裝下列項目：

    -   SQL Server 資料庫引擎上的 SSIS 目錄支援。

    -   (選擇性) SSIS Scale Out 功能，其中包含一個 Master 與若干 Worker。

    -   32 位元和 64 位元 SSIS 元件。

    -   安裝 SSIS 時，**不會**安裝設計和開發 SSIS 套件所需的工具。

-   **SQL Server 資料庫引擎**： 使用 [SQL Server 安裝精靈] 安裝資料庫引擎。 選取資料庫引擎時，可讓您建立並裝載 SSIS 目錄資料庫 (`SSISDB`)，以儲存、管理、執行及監視 SSIS 套件。

-   **SQL Server Data Tools (SSDT)**。 若要下載並安裝 SSDT，請參閱[下載 SQL Server Data Tools (SSDT)](../../ssdt/download-sql-server-data-tools-ssdt.md)。 安裝 SSDT 時，可讓您設計和部署 SSIS 套件。 SSDT 會安裝下列項目：

    -   SSIS 套件的設計和開發工具，包括 SSIS 設計工具。

    -   僅 32 位元 SSIS 元件。

    -   Visual Studio 的限制版本 (如果尚未安裝 Visual Studio 的話)。

    -   Visual Studio Tools for Applications (VSTA)，其為用於 SSIS 指令碼工作和指令碼元件的指令碼編輯器。

    -   SSIS 精靈，包括 [部署精靈] 和 [套件升級精靈]。

    -   SQL Server 匯入和匯出精靈。

-   **Integration Services Feature Pack for Azure**： 若要下載並安裝 Feature Pack，請參閱 [Microsoft SQL Server 2017 Integration Services Feature Pack for Azure](https://www.microsoft.com/download/details.aspx?id=54798)。 安裝 Feature Pack 時，可讓您的套件連線到 Azure 雲端中的儲存體和分析服務，包括下列服務：

    -   Azure Blob 儲存體。

    -   Azure HDInsight。

    -   Azure Data Lake Store。

    -   Azure SQL 資料倉儲。

-   **其他選用元件**： 您可以從 SQL Server Feature Pack 選擇性下載其他協力廠商的元件。

    -   Microsoft® Connector for SAP BW for Microsoft SQL Server®。 若要取得這些元件，請參閱 [Microsoft® SQL Server® 2017 Feature Pack](https://www.microsoft.com/download/details.aspx?id=55992)。

    -   Microsoft Connector Version 5.0 for Oracle by Attunity 和 Microsoft Connector Version 5.0 for Teradata by Attunity。 若要取得這些元件，請參閱 [Microsoft Connectors v5.0 for Oracle and Teradata](https://www.microsoft.com/download/details.aspx?id=55179)。
