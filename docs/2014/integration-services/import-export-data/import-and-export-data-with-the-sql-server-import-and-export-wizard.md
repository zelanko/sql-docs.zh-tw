---
title: SQL Server 匯入和匯出精靈 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- exporting data
- mapping files [Integration Services]
- SQL Server Import and Export Wizard
- SSIS packages, creating
- packages [Integration Services], copying
- Integration Services packages, creating
- packages [Integration Services], creating
- SQL Server Integration Services packages, creating
- Import and Export Wizard
- copying data [Integration Services]
- importing data, SSIS packages
- sources [Integration Services], copying data
ms.assetid: c0e4d867-b2a9-4b2a-844b-2fe45be88f81
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2f3ce90e2670357d0842b0a6ac7838f396465bab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62768160"
---
# <a name="sql-server-import-and-export-wizard"></a>SQL Server 匯入和匯出精靈
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]匯入和匯出精靈提供最簡單的方法，可建立[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]將資料從來源複製到目的地的封裝。  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會在 64 位元電腦上安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈 (DTSWizard.exe) 的 64 位元版本。 不過，有些資料來源 (例如，Access 或 Excel) 只有 32 位元提供者。 若要使用這些資料來源，您可能必須安裝並執行此精靈的 32 位元版本。 若要安裝此精靈的 32 位元版本，您必須在安裝期間選取用戶端工具或 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]。  
  
 您可以從 [開始] 功能表、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或命令提示字元，啟動 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 匯入和匯出精靈。 如需詳細資訊，請參閱 <<c0> [ 執行 SQL Server 匯入和匯出精靈](start-the-sql-server-import-and-export-wizard.md)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈可以在可用 Managed [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 資料提供者或原生 OLE DB 提供者的任何資料來源之間複製資料。 可用提供者的清單包括下列資料來源：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   一般檔案  
  
-   Microsoft Office Access  
  
-   Microsoft Office Excel  
  
 根據您啟動精靈的環境而定，某些精靈功能的運作方式不盡相同：  
  
-   如果您啟動[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]匯入和匯出精靈 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，您立即執行封裝選取**立即執行**核取方塊。 根據預設，此核取方塊為選取狀態，而且此封裝會立即執行。  
  
     您也可以決定要將封裝儲存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 還是檔案系統。 如果您選擇要儲存封裝，還必須指定封裝保護等級。 如需有關封裝保護等級的詳細資訊，請參閱 <<c0> [ 套件中敏感性資料的存取控制](../security/access-control-for-sensitive-data-in-packages.md)。  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈建立封裝並複製資料之後，您可以使用 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師並加入工作、轉換和事件驅動邏輯以開啟和變更已儲存的封裝。  
  
    > [!NOTE]  
    >  在 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 中，無法使用儲存此精靈所建立之封裝的選項。  
  
-   如果從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案啟動「[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 匯入和匯出精靈」，封裝將無法做為精靈完成過程中的一個步驟來執行， 而是加入到啟動精靈的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。 然後您可以執行此封裝，或透過加入工作、轉換和事件驅動邏輯 (使用 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師) 來進行擴充。  
  
 如需詳細資訊，請參閱 <<c0> [ 執行 SQL Server 匯入和匯出精靈](start-the-sql-server-import-and-export-wizard.md)。  
  
## <a name="permissions-required-by-the-import-and-export-wizard"></a>匯入和匯出精靈所需的權限  
 若要順利完成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈，您至少必須具備下列權限：  
  
-   可以連接到來源及目的地資料庫或檔案共用位置的權限。 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中，這需要伺服器與資料庫登入權限。  
  
-   可以讀取來源資料庫或檔案中之資料的權限。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，這需要來源資料表和檢視的 SELECT 權限。  
  
-   可以將資料寫入目的地資料庫或檔案的權限。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，這需要目的地資料表的 INSERT 權限。  
  
-   如果您想要建立新的目的地資料庫、資料表或檔案，就必須具備能夠建立新資料庫、資料表或檔案的足夠權限。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，這需要 CREATE DATABASE 或 CREATE TABLE 權限。  
  
-   如果您想要儲存精靈，權限不足，無法寫入 msdb 資料庫或檔案系統所建立的封裝。 在  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]，這需要 msdb 資料庫的 INSERT 權限。  
  
## <a name="mapping-data-types-in-the-import-and-export-wizard"></a>在匯入和匯出精靈中對應資料類型  
 「[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈」提供最基本的轉換功能。 除了設定新目的地資料表和檔案中資料行的名稱、資料類型和資料類型屬性之外，「[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈」不支援資料行層級的轉換。  
  
 「[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈」使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供的對應檔案，對應兩個資料庫版本或系統之間的資料類型。 例如，它可以從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 對應到 Oracle。 依預設，XML 格式的對應檔案會安裝在 C:\Program Files\Microsoft SQL Server\100\DTS\MappingFiles。 如果您的企業需要在資料類型之間進行不同的對應，您可以更新對應，以影響精靈執行的對應。 比方說，如果您想要[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **nchar**資料類型對應至 DB2**圖形**資料類型，而非 DB2 **VARGRAPHIC**傳輸資料時，資料類型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]至 DB2，變更**nchar**在 SqlClientToIBMDB2.xml 對應檔中使用對應**圖形**而非**VARGRAPHIC。**  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含許多常用來源和目的地組合之間的對應，您可以在對應檔目錄中加入新的對應檔，以支援其他來源和目的地。 新的對應檔必須符合已發行的 XSD 結構描述，並對應來源和目的地的唯一組合。  
  
> [!NOTE]  
>  如果您編輯現有的對應檔案，或將新的對應檔案加入資料夾，就必須關閉再重新開啟 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈或 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]，才能辨識新的檔案或變更後的檔案。  
  
## <a name="external-resources"></a>外部資源  
  
-   視訊[將 SQL Server 資料匯出至 Excel （SQL Server 影片）](https://go.microsoft.com/fwlink/?LinkID=200975)，technet.microsoft.com 上的  
  
-   CodePlex 範例：[從 ODBC 匯出到一般檔案使用精靈教學課程：課程封裝](https://go.microsoft.com/fwlink/?LinkId=217657)，位於 msftisprodsamples.codeplex.com  
  
  
