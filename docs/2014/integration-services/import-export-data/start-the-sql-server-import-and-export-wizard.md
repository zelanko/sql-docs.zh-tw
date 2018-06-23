---
title: 執行 SQL Server 匯入和匯出精靈 |Microsoft 文件
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL Server Import and Export Wizard
- starting SQL Server Import and Export Wizard
- Import and Export Wizard
- starting Import and Export Wizard
ms.assetid: 5fc4f6d1-1f6f-444e-9aeb-827f85e1c405
caps.latest.revision: 67
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 817172e78c7f7702aa4dc9d7555b25f6866a6897
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36145422"
---
# <a name="run-the-sql-server-import-and-export-wizard"></a>執行 SQL Server 匯入和匯出精靈
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈提供最簡單的方法，讓您在資料來源之間複製資料以及建構基本封裝。 如需有關精靈的詳細資訊，請參閱[SQL Server 匯入和匯出精靈](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。  
  
 如需示範如何使用 SQL Server 匯入和匯出精靈建立的封裝，將資料從 SQL Server 資料庫匯出至 Microsoft Excel 試算表的影片，請參閱[SQL Server 資料匯出到 Excel （SQL Server 視訊）](http://go.microsoft.com/fwlink/?LinkId=131024)。  
  
### <a name="to-start-the-sql-server-import-and-export-wizard"></a>若要啟動 SQL Server 匯入和匯出精靈  
  
-   在**啟動**功能表上，指向**所有程式**，指向 **Microsoft SQL Server** ，然後按一下 **匯入和匯出資料**。  
  
     – 或 –  
  
     在[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]，以滑鼠右鍵按一下**SSIS 封裝**資料夾，然後再按一下**SSISImport 和匯出精靈**。  
  
     – 或 –  
  
     在[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]上**專案**功能表上，按一下  **SSISImport 和匯出精靈**。  
  
     – 或 –  
  
     在[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，連接到[!INCLUDE[ssDE](../../includes/ssde-md.md)]伺服器類型，展開資料庫，請以滑鼠右鍵按一下資料庫，指向**工作**，然後按一下 **匯入資料**或**匯出資料**.  
  
     – 或 –  
  
     在命令提示字元視窗中，執行 DTSWizard.exe (位於 C:\Program Files\Microsoft SQL Server\100\DTS\Binn)。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會在 64 位元電腦上安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈 (DTSWizard.exe) 的 64 位元版本。 不過，有些資料來源 (例如，Access 或 Excel) 只有 32 位元提供者。 若要使用這些資料來源，您可能必須安裝並執行此精靈的 32 位元版本。 若要安裝 32 位元版本的精靈，選取 用戶端工具或[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]在安裝期間。  
  
### <a name="to-import-or-export-data-by-using-the-sql-server-import-and-export-wizard"></a>使用 SQL Server 匯入和匯出精靈來匯入或匯出資料  
  
1.  啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈。  
  
2.  在對應的精靈頁面上，選取資料來源和資料目的地。  
  
     可用的資料來源包括 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 資料提供者、OLE DB 提供者、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 提供者、[!INCLUDE[vstecado](../../includes/vstecado-md.md)] 提供者、Microsoft Office Excel、Microsoft Office Access 和一般檔案來源。 視來源而定，您可以設定驗證模式、伺服器名稱、資料庫名稱和檔案格式等選項。  
  
    > [!NOTE]  
    >  [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for Oracle 不支援 Oracle BLOB、CLOB、NCLOB、BFILE 和 UROWID 等資料類型。 因此，OLE DB 來源不能從包含這些資料類型之資料行的資料表中擷取資料。  
  
     可用的資料目的地包括[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]資料提供者、 OLE DB 提供者、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client、 Excel、 Access 和一般檔案目的地。  
  
3.  設定選取之目的地類型的選項。  
  
     如果目的地為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫，您可以指定下列項目：  
  
    -   指示是否要新建資料庫並設定資料庫屬性。 下列屬性無法進行設定，精靈將使用指定的預設值：  
  
        |屬性|ReplTest1|  
        |--------------|-----------|  
        |定序|Latin1_General_CS_AS_KS_WS|  
        |復原模式|完整|  
        |使用全文檢索索引|True|  
  
    -   選擇是要從資料表或檢視表複製資料，還是複製查詢結果。  
  
         若要查詢來源資料並複製結果，可以建構 Transact-SQL 查詢。 您可以手動輸入 Transact-SQL 查詢，或使用儲存到檔案的查詢。 此精靈包含用來尋找檔案的瀏覽功能，還可在您選取檔案時自動開啟檔案，並將其內容貼到精靈頁面。  
  
         如果來源為 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 提供者，您還可以使用複製查詢結果的選項，提供 DBCommand 字串當做查詢。  
  
         如果來源資料 檢視中，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]匯入和匯出精靈 」 自動將檢視轉換至目的地中的資料表。  
  
    -   指示是否卸除並重新建立目的地資料表，以及是否啟用識別插入。  
  
    -   指示是要刪除資料列，還是在現有的目的地資料表內附加資料列。 如果資料表不存在，「[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈」會自動予以建立。  
  
     如果目的地為一般檔案目的地，您可以指定下列項目：  
  
    -   指定目的地檔案中的資料列分隔符號。  
  
    -   指定目的地檔案中的資料行分隔符號。  
  
4.  (選擇性) 選取一個資料表並變更來源和目的地資料行之間的對應，或變更目的地資料行的中繼資料：  
  
    -   將來源資料行對應到不同的目的地資料行。  
  
    -   變更目的地資料行中的資料類型。  
  
    -   設定具有字元資料類型之資料行的長度。  
  
    -   設定具有數值資料類型之資料行的有效位數和小數位數。  
  
    -   指定資料行是否可包含 Null 值。  
  
5.  (選擇性) 選取多個資料表，並更新套用至這些資料表的中繼資料和選項：  
  
    -   選取現有的目的地結構描述，或提供要指派資料表的新結構描述。  
  
    -   指定目的地資料表中是否啟用識別插入。  
  
    -   指定是否要卸除目的地資料表，然後重建。  
  
    -   指定是否要截斷現有的目的地資料表。  
  
6.  儲存並執行封裝。  
  
     如果從 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或命令提示字元啟動精靈，此封裝便可立即執行。 您可以選擇性地將封裝儲存到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **msdb**資料庫或檔案系統。 如需有關**msdb**資料庫，請參閱[封裝管理&#40;SSIS 服務&#41;](../service/package-management-ssis-service.md)。  
  
     當您儲存封裝時，可以設定封裝保護等級，而如果保護等級使用密碼，請提供密碼。 如需有關封裝保護等級的詳細資訊，請參閱[封裝中的機密資料的存取控制](../security/access-control-for-sensitive-data-in-packages.md)。  
  
     如果啟動精靈從[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]專案中[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]，您無法從精靈執行封裝。 而是加入到啟動精靈的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。 然後您可以在執行封裝[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]。  
  
    > [!NOTE]  
    >  在[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]，就無法使用儲存精靈所建立的封裝選項。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 匯入和匯出精靈](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)   
 [在 SQL Server Data Tools 中建立套件](../create-packages-in-sql-server-data-tools.md)  
  
  