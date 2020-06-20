---
title: 檔案系統工作編輯器（一般頁面） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.filesystemtask.general.f1
helpviewer_keywords:
- File System Task Editor
ms.assetid: 51fe6614-3418-4eff-a28d-02ea31cc9aa9
author: janinezhang
ms.author: janinez
ms.openlocfilehash: cf0c153168c513c98f8b9ac58984cb88ae1811da
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84967128"
---
# <a name="file-system-task-editor-general-page"></a>檔案系統工作編輯器 (一般頁面)
  使用 [檔案系統工作編輯器]**** 對話方塊的 [一般]**** 頁面，即可設定工作執行的檔案系統作業。  
  
 若要了解這項工作，請參閱 [檔案系統工作](control-flow/file-system-task.md)。  
  
 您必須透過設定 SourceConnection 和 DestinationConnection 屬性，以指定來源和目的地連線管理員。 您可以提供指向工作做為來源或目的地使用之檔案的檔案連接管理員名稱，而如果檔案路徑是儲存在變數中，則可以提供變數的名稱。 若要使用變數來儲存檔案路徑，您必須先將來源連接的 [IsSourcePathVariable] 選項和目的地連接的 [IsDestinationPatheVariable] 選項設定為 [True]****。 接著您就可以選擇要使用的現有系統或使用者自訂變數，或是建立新的變數。 您可以在 [加入變數]**** 對話方塊中，設定和指定變數的範圍。 此範圍必須是「檔案系統」工作或父容器。 如需詳細資訊，請參閱[Integration Services &#40;SSIS&#41; 變數](integration-services-ssis-variables.md)，並[在封裝中使用變數](../../2014/integration-services/use-variables-in-packages.md)。  
  
> [!NOTE]  
>  若要覆寫您為和屬性選取的變數 `SourceConnection` `DestinationConnection` ，請在 [**來源**] 和 [**目的地**] 屬性中輸入運算式。 您可在 [檔案系統工作編輯器]**** 的 [運算式]**** 頁面上輸入運算式。 例如，為了設定做為工作目的地使用的檔案路徑，在某些情況下您可能想要使用變數 A，而在其他情況下使用變數 B。  
  
> [!NOTE]  
>  「檔案系統」工作會在單一檔案或目錄上運作。 因此，這項工作不支援使用萬用字元在多個檔案或目錄上執行相同的作業。 為了要讓「檔案系統」工作在多個檔案或目錄上重複作業，請將此「檔案系統」工作放入 Foreach 迴圈容器內。 如需詳細資訊，請參閱 [檔案系統工作](control-flow/file-system-task.md)。  
  
 您可以使用運算式，將不同的變數用於  
  
## <a name="options"></a>選項。  
 **IsDestinationPathVariable**  
 指出目的地路徑是否儲存在變數中。 這個屬性具有下表中所列的選項。  
  
|值|描述|  
|-----------|-----------------|  
|**真正**|目的地路徑儲存在變數中。 選取這個值會顯示動態選項 [DestinationVariable]****。|  
|**False**|目的地路徑是在檔案連接管理員中指定。 選取此值會顯示動態選項： `DestinationConnection` 。|  
  
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
|**移動檔案**|移動檔案。 選取此值會顯示來源與目的地的動態選項。<br /><br /> 注意：移動檔案時，請勿在您提供作為目的地的目錄路徑中包含檔案名。|  
|**重新命名檔案**|重新命名檔案。 選取此值會顯示來源與目的地的動態選項。<br /><br /> 注意：重新命名檔案時，請在您提供給目的地的目錄路徑中包含新的檔案名。|  
|**設定屬性**|設定檔案或目錄的屬性。 選取此值會顯示來源與作業的動態選項。|  
  
 `IsSourcePathVariable`  
 指出目的地路徑是否儲存在變數中。 這個屬性具有下表中所列的選項。  
  
|值||  
|-----------|-|  
|**真正**|目的地路徑儲存在變數中。 選取此值會顯示動態選項 [SourceVariable]****。|  
|**False**|目的地路徑是在檔案連接管理員中指定。 選取這個值會顯示動態選項 [DestinationVariable]****。|  
  
## <a name="isdestinationpathvariable-dynamic-options"></a>IsDestinationPathVariable 動態選項  
  
### <a name="isdestinationpathvariable--true"></a>IsDestinationPathVariable = True  
 **DestinationVariable**  
 在清單中選取變數名稱，或按一下 \<**New variable...**> 以建立新的變數。  
  
 **相關主題：** [Integration Services &#40;SSIS&#41; 變數](integration-services-ssis-variables.md)、[新增變數](../../2014/integration-services/add-variable.md)  
  
### <a name="isdestinationpathvariable--false"></a>IsDestinationPathVariable = False  
 `DestinationConnection`  
 在清單中選取檔案連線管理員，或按一下 \<**New connection...**> 以建立新的連線管理員。  
  
 **相關主題：** [File Connection Manager](connection-manager/file-connection-manager.md)、 [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
## <a name="issourcepathvariable-dynamic-options"></a>IsSourcePathVariable 動態選項  
  
### <a name="issourcepathvariable--true"></a>IsSourcePathVariable = True  
 **SourceVariable**  
 在清單中選取變數名稱，或按一下 \<**New variable...**> 以建立新的變數。  
  
 **相關主題：** [Integration Services &#40;SSIS&#41; 變數](integration-services-ssis-variables.md)、[新增變數](../../2014/integration-services/add-variable.md)  
  
### <a name="issourcepathvariable--false"></a>IsSourcePathVariable = False  
 `SourceConnection`  
 在清單中選取檔案連線管理員，或按一下 \<**New connection...**> 以建立新的連線管理員。  
  
 **相關主題：** [File Connection Manager](connection-manager/file-connection-manager.md)、 [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
## <a name="operation-dynamic-options"></a>作業動態選項  
  
### <a name="operation--set-attributes"></a>作業 = 設定屬性  
 **隱含**  
 指出檔案或目錄是否可見。  
  
 **ReadOnly**  
 指出檔案是否為唯讀。  
  
 **存檔**  
 指出檔案或目錄是否準備就緒，可供封存。  
  
 **系統**  
 指出檔案是否為作業系統檔案。  
  
### <a name="operation--create-directory"></a>作業 = 建立目錄  
 `UseDirectoryIfExists`  
 指出 [建立目錄]**** 作業是否會使用具有指定之名稱的現有目錄，而不是建立新的目錄。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [運算式頁面](expressions/expressions-page.md)  
  
  
