---
title: 檔案系統工作 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.filesystemtask.f1
- sql13.dts.designer.filesystemtask.general.f1
helpviewer_keywords:
- File System task [Integration Services]
ms.assetid: 7dd79a6a-e066-4028-a385-1d40f31056f8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 77a347078f86299118f80c9cae55d9dd04795a9d
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86917894"
---
# <a name="file-system-task"></a>檔案系統工作

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  「檔案系統」工作會在檔案系統中的檔案和目錄上執行作業。 例如，封裝可使用「檔案系統」工作建立、移動或刪除目錄和檔案。 您也可以使用「檔案系統」工作設定檔案和目錄的屬性。 例如，「檔案系統」工作可將檔案設為隱藏或唯讀。  
  
 所有「檔案系統」工作作業均使用來源，其可為檔案或目錄。 例如，工作所複製的檔案或刪除的目錄即為來源。 來源可使用指向目錄或檔案的「檔案」連接管理員指定，或藉由提供包含來源路徑的變數名稱指定。 如需詳細資訊，請參閱[檔案連線管理員](../../integration-services/connection-manager/file-connection-manager.md)和 [Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)。  
  
 複製和移動檔案與目錄以及重新命名檔案的作業會使用目的地和來源。 目的地是使用「檔案」連接管理員或變數指定。 檔案系統工作的作業可設定為允許覆寫目的地檔案和目錄。 建立新目錄的作業可設定為當目錄已存在時使用具有指定名稱的現有目錄，而不會失敗。  
  
## <a name="predefined-file-system-operations"></a>預先定義的檔案系統作業  
 「檔案系統」工作包括一組預先定義的作業。 下表描述這些作業。  
  
|作業|描述|  
|---------------|-----------------|  
|複製目錄|將資料夾從一個位置複製到另一個。|  
|複製檔案|將檔案從一個位置複製到另一個。|  
|建立目錄|在指定的位置建立資料夾。|  
|刪除目錄|刪除指定位置的資料夾。|  
|刪除目錄內容|刪除某個資料夾中的所有檔案和資料夾。|  
|刪除檔案|刪除指定位置的檔案。|  
|移動目錄|將資料夾從一個位置移到另一個。|  
|移動檔案|將檔案從一個位置移到另一個。|  
|重新命名檔案|重新命名指定位置的檔案。|  
|設定屬性|設定檔案和資料夾的屬性。 屬性包括「封存」、「隱藏」、「一般」「唯讀」和「系統」。 「一般」表示無任何屬性，且不可與其他屬性結合。 其他所有屬性都可互相結合使用。|  
  
 「檔案系統」工作會在單一檔案或目錄上運作。 因此，這項工作不支援使用萬用字元在多個檔案上執行相同的作業。 為了要讓「檔案系統」工作在多個檔案或目錄上重複作業，請將「檔案系統」工作放入 Foreach 迴圈容器內，如以下步驟所述：  
  
-   **設定 Foreach 迴圈容器** ：在 [Foreach 迴圈編輯器] 的 **[集合]** 頁面上，將列舉值設定為 **[Foreach 檔案列舉值]** 然後輸入萬用字元運算式，做為 **[檔案]** 的列舉值組態。 在 [Foreach 迴圈編輯器] 的 **[變數對應]** 頁面上，對應您要使用的變數，以便將檔案名稱傳遞到 [檔案系統] 工作，一次一個。  
  
-   **加入和設定檔案系統工作** ：將「檔案系統」工作加入到「Foreach 迴圈」容易。 在「檔案系統工作編輯器」的 **[一般]** 頁面上，將 **[SourceVariable]** 或 **[DestinationVariable]** 屬性設定為您在「Foreach 迴圈」容器中定義的變數。  
  
## <a name="custom-log-entries-available-on-the-file-system-task"></a>檔案系統工作上可用的自訂記錄項目  
 下表描述「檔案系統」工作的自訂記錄項目。 如需詳細資訊，請參閱 [集成服務 &#40;SSIS&#41; 記錄](../../integration-services/performance/integration-services-ssis-logging.md)。  
  
|記錄項目|描述|  
|---------------|-----------------|  
|**FileSystemOperation**|報告工作執行的作業。 記錄項目會在檔案系統作業開始時寫入，項目中包含有關來源和目的地的資訊。|  
  
## <a name="configuring-the-file-system-task"></a>設定檔案系統工作  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需有關可在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定之屬性的詳細資訊，請參閱下列主題：  
  
-   [檔案系統工作編輯器 &#40;一般頁面&#41;](../../integration-services/control-flow/file-system-task-editor-general-page.md)  
  
-   [運算式頁面](../../integration-services/expressions/expressions-page.md)  
  
 如需有關如何在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定這些屬性的詳細資訊，請參閱下列主題：  
  
-   [設定工作或容器的屬性](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
 如需有關如何以程式設計的方式設定這些屬性的詳細資訊，請參閱下列主題：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask>  
  
## <a name="related-tasks"></a>相關工作  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包括下載和上傳資料檔以及管理伺服器上目錄的工作。 如需相關資訊，請參閱 [FTP Task](../../integration-services/control-flow/ftp-task.md)。  
  
## <a name="file-system-task-editor-general-page"></a>檔案系統工作編輯器 (一般頁面)
  使用 [檔案系統工作編輯器]  對話方塊的 [一般]  頁面，即可設定工作執行的檔案系統作業。  
  
 您必須透過設定 SourceConnection 和 DestinationConnection 屬性，以指定來源和目的地連線管理員。 您可以提供指向工作做為來源或目的地使用之檔案的檔案連接管理員名稱，而如果檔案路徑是儲存在變數中，則可以提供變數的名稱。 若要使用變數來儲存檔案路徑，您必須先將來源連接的 [IsSourcePathVariable] 選項和目的地連接的 [IsDestinationPatheVariable] 選項設定為 [True]  。 接著您就可以選擇要使用的現有系統或使用者自訂變數，或是建立新的變數。 您可以在 [加入變數]  對話方塊中，設定和指定變數的範圍。 此範圍必須是「檔案系統」工作或父容器。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)和[在封裝中使用變數](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)。  
  
> [!NOTE]  
>  若要覆寫您針對 **SourceConnection** 和 **DestinationConnection** 屬性選取的變數，請針對 [來源]  和 [目的地]  屬性輸入運算式。 您可在 [檔案系統工作編輯器]  的 [運算式]  頁面上輸入運算式。 例如，為了設定做為工作目的地使用的檔案路徑，在某些情況下您可能想要使用變數 A，而在其他情況下使用變數 B。  
  
> [!NOTE]  
>  「檔案系統」工作會在單一檔案或目錄上運作。 因此，這項工作不支援使用萬用字元在多個檔案或目錄上執行相同的作業。 為了要讓「檔案系統」工作在多個檔案或目錄上重複作業，請將此「檔案系統」工作放入 Foreach 迴圈容器內。 如需詳細資訊，請參閱 [檔案系統工作](../../integration-services/control-flow/file-system-task.md)。  
  
 您可以使用運算式，將不同的變數用於  
  
### <a name="options"></a>選項。  
 **IsDestinationPathVariable**  
 指出目的地路徑是否儲存在變數中。 這個屬性具有下表中所列的選項。  
  
|值|描述|  
|-----------|-----------------|  
|**True**|目的地路徑儲存在變數中。 選取這個值會顯示動態選項 [DestinationVariable]  。|  
|**False**|目的地路徑是在檔案連接管理員中指定。 選取這個值會顯示動態選項 [DestinationConnection]  。|  
  
 **OverwriteDestination**  
 指定作業是否可覆寫目的地目錄中的檔案。  
  
 **名稱**  
 為檔案系統工作提供唯一的名稱。 這個名稱是作為工作圖示中的標籤使用。  
  
> [!NOTE]  
>  工作名稱在封裝內必須是唯一的。  
  
 **說明**  
 輸入檔案系統工作的描述。  
  
 **運算**  
 選取要執行的檔案系統作業。 這個屬性具有下表中所列的選項。  
  
|值|描述|  
|-----------|-----------------|  
|**複製目錄**|複製目錄。 選取此值會顯示來源與目的地的動態選項。|  
|**複製檔案**|複製檔案。 選取此值會顯示來源與目的地的動態選項。|  
|**建立目錄**|建立目錄。 選取此值會顯示來源和目的地目錄的動態選項。|  
|**刪除目錄**|刪除目錄。 選取此值會顯示來源的動態選項。|  
|**刪除目錄內容**|刪除目錄的內容。 選取此值會顯示來源的動態選項。|  
|**刪除檔案**|刪除檔案。 選取此值會顯示來源的動態選項。|  
|**移動目錄**|移動目錄。 選取此值會顯示來源與目的地的動態選項。|  
|**移動檔案**|移動檔案。 選取此值會顯示來源與目的地的動態選項。 當移動檔案時，請勿在您提供當做目的地的目錄路徑內包含檔案名稱。|  
|**重新命名檔案**|重新命名檔案。 選取此值會顯示來源與目的地的動態選項。 當重新命名檔案時，請在您提供當做目的地的目錄路徑內包含新的檔案名稱。|  
|**設定屬性**|設定檔案或目錄的屬性。 選取此值會顯示來源與作業的動態選項。|  
  
 **IsSourcePathVariable**  
 指出目的地路徑是否儲存在變數中。 這個屬性具有下表中所列的選項。  
  
|值||  
|-----------|-|  
|**True**|目的地路徑儲存在變數中。 選取此值會顯示動態選項 [SourceVariable]  。|  
|**False**|目的地路徑是在檔案連接管理員中指定。 選取這個值會顯示動態選項 [DestinationVariable]  。|  
  
### <a name="isdestinationpathvariable-dynamic-options"></a>IsDestinationPathVariable 動態選項  
  
#### <a name="isdestinationpathvariable--true"></a>IsDestinationPathVariable = True  
 **DestinationVariable**  
 選取清單中的變數名稱，或按一下 \<**New variable...**> 建立新的變數。  
  
 **相關主題：** [Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)、[新增變數](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
#### <a name="isdestinationpathvariable--false"></a>IsDestinationPathVariable = False  
 **DestinationConnection**  
 在清單中選取檔案連線管理員，或按一下 \<**New connection...**> 來建立新的連線管理員。  
  
 **相關主題：** [檔案連線管理員](../../integration-services/connection-manager/file-connection-manager.md)、[檔案連線管理員編輯器](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
### <a name="issourcepathvariable-dynamic-options"></a>IsSourcePathVariable 動態選項  
  
#### <a name="issourcepathvariable--true"></a>IsSourcePathVariable = True  
 **SourceVariable**  
 選取清單中的變數名稱，或按一下 \<**New variable...**> 建立新的變數。  
  
 **相關主題：** [Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)、[新增變數](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
#### <a name="issourcepathvariable--false"></a>IsSourcePathVariable = False  
 **SourceConnection**  
 在清單中選取檔案連線管理員，或按一下 \<**New connection...**> 來建立新的連線管理員。  
  
 **相關主題：** [檔案連線管理員](../../integration-services/connection-manager/file-connection-manager.md)  
  
### <a name="operation-dynamic-options"></a>作業動態選項  
  
#### <a name="operation--set-attributes"></a>作業 = 設定屬性  
 **Hidden**  
 指出檔案或目錄是否可見。  
  
 **ReadOnly**  
 指出檔案是否為唯讀。  
  
 **封存**  
 指出檔案或目錄是否準備就緒，可供封存。  
  
 **系統**  
 指出檔案是否為作業系統檔案。  
  
#### <a name="operation--create-directory"></a>作業 = 建立目錄  
 **UseDirectoryIfExists**  
 指出 [建立目錄]  作業是否會使用具有指定之名稱的現有目錄，而不是建立新的目錄。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 工作](../../integration-services/control-flow/integration-services-tasks.md)   
 [控制流程](../../integration-services/control-flow/control-flow.md)  
  
  
