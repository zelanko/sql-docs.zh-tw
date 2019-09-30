---
title: ADO NET 來源 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.adonetsource.f1
- sql13.dts.designer.adonetsource.connection.f1
- sql13.dts.designer.adonetsource.columns.f1
- sql13.dts.designer.adonetsource.erroroutput.f1
helpviewer_keywords:
- ADO.NET source
- sources [Integration Services], ADO.NET
- sources [Integration Services], DataReader
- .NET Framework [Integration Services]
- DataReader source
ms.assetid: 2a2f1750-2cda-4dda-9dca-623a96a6b3c0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ade0d29ed20bb8b39d9ac2a1762977abe24d8f65
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2019
ms.locfileid: "71293518"
---
# <a name="ado-net-source"></a>ADO NET 來源

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  ADO NET 來源會從 .NET 提供者取用資料，並使該資料可供資料流程使用。  
  
 您可以使用 ADO NET 來源連接至 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]。 不過，不支援使用 OLE DB 連接到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 。 如需 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 的詳細資訊，請參閱[一般指導方針與限制 (Azure SQL Database)](https://go.microsoft.com/fwlink/?LinkId=248228)。  
  
## <a name="data-type-support"></a>資料類型支援  
 此來源會將未對應到特定 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 資料類型的所有資料類型轉換成 DT_NTEXT [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 資料類型。 即使資料類型為 **System.Object**，還是會發生轉換。  
  
 您可以將 DT_NTEXT 資料類型變更為 DT_WSTR 資料類型，或是將 DT_WSTR 資料類型變更為 DT_NTEXT 資料類型。 您可以在 ADO NET 來源的 **[進階編輯器]** 對話方塊中設定 **[DataType]** 屬性，以變更資料類型。 如需詳細資訊，請參閱 [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)。  
  
 您可以在 ADO NET 來源之後使用資料轉換，將 DT_NTEXT 資料類型轉換成 DT_BYTES 或 DT_STR 資料類型。 如需詳細資訊，請參閱 [Data Conversion Transformation](../../integration-services/data-flow/transformations/data-conversion-transformation.md)。  
  
 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]中，資料類型 DT_DBDATE、DT_DBTIME2、DT_DBTIMESTAMP2 和 DT_DBTIMESTAMPOFFSET 會對應到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的某些日期資料類型。 您可以設定 ADO NET 來源，從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用的日期資料類型轉換成 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 使用的資料類型。 如果要設定 ADO NET 來源，以轉換這些日期資料類型，請將 **連接管理員的** [Type System Version] [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 屬性設定為 **[Latest]** 。 (**Type System Version** 屬性位於 [連線管理員]  對話方塊的 [全部]  頁面上。 若要開啟 [連線管理員]  對話方塊，請以滑鼠右鍵按一下 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連線管理員，然後按一下 [編輯]  。)  
  
> [!NOTE]  
>  如果 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連線管理員的 **Type System Version** 屬性設定為 **SQL Server 2005**，系統會將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型轉換成 DT_WSTR。  
  
 當 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 連線管理員將提供者指定為 .NET Data Provider for [!INCLUDE[vstecado](../../includes/vstecado-md.md)] (SqlClient) 時，系統會將使用者定義資料類型 (UDT) 轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 二進位大型物件 (BLOB)。 當系統轉換 UDT 資料類型時，會套用以下規則：  
  
-   如果資料不是大型 UDT，系統會將資料轉換成 DT_BYTES。  
  
-   如果資料不是大型 UDT，而且資料庫上資料行的 **Length** 屬性設定為 -1 或是大於 8,000 個位元組的值，則系統會將資料轉換成 DT_IMAGE。  
  
-   如果資料是大型 UDT，系統會將資料轉換成 DT_IMAGE。  
  
    > [!NOTE]  
    >  如果 ADO NET 來源未設定為使用錯誤輸出，系統會將資料流向 DT_IMAGE 資料行 (以 8,000 個位元組的區塊為單位)。 如果 ADO NET 來源設定為使用錯誤輸出，系統會將整個位元組陣列傳遞給 DT_IMAGE 資料行。 如需如何設定元件使用錯誤輸出的詳細資訊，請參閱 [處理資料中的錯誤](../../integration-services/data-flow/error-handling-in-data.md)。  
  
 如需 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 資料類型、支援的資料類型轉換及橫跨某些資料庫 (包括 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) 之資料類型對應的詳細資訊，請參閱 [Integration Services 資料類型](../../integration-services/data-flow/integration-services-data-types.md)。  
  
 如需將 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 資料類型對應至 Managed 資料類型的詳細資訊，請參閱 [使用資料流程中的資料類型](../../integration-services/extending-packages-custom-objects/data-flow/working-with-data-types-in-the-data-flow.md)。  
  
## <a name="ado-net-source-troubleshooting"></a>疑難排解 ADO NET 來源  
 您可以記錄 ADO NET 來源對外部資料提供者所執行的呼叫。 您可以使用這項記錄功能，疑難排解 ADO NET 來源執行的從外部資料來源載入資料的作業。 若要記錄 ADO NET 來源對外部資料提供者執行的呼叫，請啟用封裝記錄，然後在封裝層級上選取 **[診斷]** 事件。 如需詳細資訊，請參閱 [封裝執行的疑難排解工具](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)。  
  
## <a name="ado-net-source-configuration"></a>ADO NET 來源組態  
 您可藉由提供定義結果集的 SQL 陳述式，以設定 ADO NET 來源。 例如，連接到 [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 資料庫並使用 SQL 陳述式 `SELECT * FROM Production.Product` 的 ADO NET 來源會從 **Production.Product** 資料表擷取所有資料列，並提供資料集給下游元件。  
  
> [!NOTE]  
>  當您使用 SQL 陳述式呼叫從暫存資料表傳回結果的預存程序時，請使用 WITH RESULT SETS 選項定義結果集的中繼資料。  
  
> [!NOTE]  
>  如果您使用 SQL 陳述式執行預存程序，封裝就會失敗且出現下列錯誤。透過在 exec 陳述式前面加上 **SET FMTONLY OFF** 陳述式也許能夠解決這項錯誤。  
>   
>  **在資料來源中找不到資料行 <資料行名稱>。**  
  
 ADO NET 來源會使用 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連接管理員連接到資料來源，且由連接管理員指定 .NET 提供者。 如需詳細資訊，請參閱 [ADO.NET Connection Manager](../../integration-services/connection-manager/ado-net-connection-manager.md)。  
  
 ADO NET 來源有一個一般輸出和一個錯誤輸出。  
  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [ADO NET 自訂屬性](../../integration-services/data-flow/ado-net-custom-properties.md)  
  
 如需如何設定屬性的詳細資訊，請參閱 [設定資料流程元件的屬性](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="ado-net-source-editor-connection-manager-page"></a>ADO NET 來源編輯器 (連接管理員頁面)
  使用 [ADO NET 來源編輯器]  對話方塊的 [連線管理員]  頁面，即可選取來源的 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連線管理員。 這個頁面也可以讓您從資料庫中選取資料表或檢視。  
  
 若要深入了解 ADO NET 來源，請參閱＜ [ADO NET Source](../../integration-services/data-flow/ado-net-source.md)＞。  
  
 **開啟連接管理員頁面**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟具有 ADO NET 來源的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。  
  
2.  在 [資料流程]  索引標籤中，按兩下 ADO NET 來源。  
  
3.  在 [ADO NET 來源編輯器]  中，按一下 [連線管理員]  。  
  
### <a name="static-options"></a>靜態選項  
 **ADO.NET 連接管理員**  
 從清單中選取現有的連線管理員，或按一下 [新增]  來建立新的連線。  
  
 **新增**  
 使用 [設定 ADO.NET 連線管理員]  對話方塊建立新的連線管理員。  
  
 **資料存取模式**  
 從來源中指定選取資料的方法。  
  
|選項|Description|  
|------------|-----------------|  
|資料表或檢視|從 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 資料來源中的資料表或檢視擷取資料。|  
|SQL (命令)|使用 SQL 查詢從 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 資料來源中擷取資料。|  
  
 **預覽**  
 使用 [資料檢視]  對話方塊來預覽結果。 [預覽]  最多可顯示 200 個資料列。  
  
> [!NOTE]  
>  在預覽資料時，具有 CLR 使用者定義型別的資料行不會包含資料。 而會顯示 \<數值太大而無法顯示> 或 System.Byte[]。 使用 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 提供者存取資料來源時會顯示前者，而使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 提供者時會顯示後者。  
  
### <a name="data-access-mode-dynamic-options"></a>資料存取模式動態選項  
  
#### <a name="data-access-mode--table-or-view"></a>資料存取模式 = 資料表或檢視  
 **資料表或檢視的名稱**  
 從資料來源中可用的清單中選取資料表或檢視名稱。  
  
#### <a name="data-access-mode--sql-command"></a>資料存取模式 = SQL 命令  
 **SQL 命令文字**  
 輸入 SQL 查詢文字，按一下 [建立查詢]  建立查詢，或按一下 [瀏覽]  找到包含查詢文字的檔案。  
  
 **建立查詢**  
 使用 [查詢產生器]  對話方塊，以視覺化的方式來建構 SQL 查詢。  
  
 **瀏覽**  
 使用 [開啟]  對話方塊來找出包含 SQL 查詢文字的檔案。  
  
## <a name="ado-net-source-editor-columns-page"></a>ADO NET 來源編輯器 (資料行頁面)
  使用 [ADO NET 來源編輯器]  對話方塊的 [資料行]  頁面，即可將輸出資料行對應至每個外部 (來源) 資料行。  
  
 若要深入了解 ADO NET 來源，請參閱＜ [ADO NET Source](../../integration-services/data-flow/ado-net-source.md)＞。  
  
 **開啟資料行頁面**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟具有 ADO NET 來源的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。  
  
2.  在 [資料流程]  索引標籤上，按兩下 ADO NET 來源。  
  
3.  在 **[ADO NET 來源編輯器]** 中，按一下 **[資料行]** 。  
  
### <a name="options"></a>選項。  
 **可用的外部資料行**  
 在資料來源中檢視可用的外部資料行清單。 您無法使用此資料表來加入或刪除資料行。  
  
 **[外部資料行]**  
 依您在設定使用此來源之資料的元件時所見的順序來檢視外部 (來源) 資料行。  
  
 **輸出資料行**  
 為每個輸出資料行提供唯一的名稱。 預設值為選取的外部 (來源) 資料行的名稱；不過，您也可以選擇任何唯一的、描述性的名稱。 提供的名稱將顯示在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師內。  
  
## <a name="ado-net-source-editor-error-output-page"></a>ADO NET 來源編輯器 (錯誤輸出頁面)
  使用 [ADO NET 來源編輯器]  對話方塊的 [錯誤輸出]  頁面，即可選取錯誤處理選項，並設定錯誤輸出資料行的屬性。  
  
 若要深入了解 ADO NET 來源，請參閱＜ [ADO NET Source](../../integration-services/data-flow/ado-net-source.md)＞。  
  
 **開啟錯誤輸出頁面**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟具有 ADO NET 來源的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。  
  
2.  在 [資料流程]  索引標籤上，按兩下 ADO NET 來源。  
  
3.  在 [ADO NET 來源編輯器]  中，按一下 [錯誤輸出]  。  
  
### <a name="options"></a>選項。  
 **輸入/輸出**  
 檢視資料來源的名稱。  
  
 **資料行**  
 檢視您在 [ADO NET 來源編輯器]  對話方塊之 [連接管理員]  頁面上所選取的外部 (來源) 資料行。  
  
 **錯誤**  
 指定錯誤發生時要採取的動作：忽略失敗、重新導向資料列，或使元件失效。  
  
 **相關主題：** [資料中的錯誤處理](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **截斷**  
 指定截斷發生時要採取的動作：忽略失敗、重新導向資料列，或使元件失效。  
  
 **說明**  
 檢視錯誤的描述。  
  
 **將這個值設定到選取的資料格**  
 指定發生錯誤或截斷時要對所有選取之資料格採取的動作：忽略失敗、重新導向資料列，或使元件失效。  
  
 **套用**  
 將錯誤處理選項套用至選取的資料格。  
  
## <a name="see-also"></a>另請參閱  
 [DataReader 目的地](../../integration-services/data-flow/datareader-destination.md)   
 [ADO NET 目的地](../../integration-services/data-flow/ado-net-destination.md)   
 [資料流程](../../integration-services/data-flow/data-flow.md)  
  
  
