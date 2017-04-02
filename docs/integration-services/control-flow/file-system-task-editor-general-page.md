---
title: "檔案系統工作編輯器 (一般頁面) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.filesystemtask.general.f1"
helpviewer_keywords: 
  - "檔案系統工作編輯器"
ms.assetid: 51fe6614-3418-4eff-a28d-02ea31cc9aa9
caps.latest.revision: 43
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 43
---
# 檔案系統工作編輯器 (一般頁面)
  使用 [檔案系統工作編輯器] 對話方塊的 [一般] 頁面，即可設定工作執行的檔案系統作業。  
  
 若要了解這項工作，請參閱[檔案系統工作](../../integration-services/control-flow/file-system-task.md)。  
  
 您必須透過設定 SourceConnection 和 DestinationConnection 屬性，以指定來源和目的地連線管理員。 您可以提供指向工作做為來源或目的地使用之檔案的檔案連接管理員名稱，而如果檔案路徑是儲存在變數中，則可以提供變數的名稱。 若要使用變數來儲存檔案路徑，您必須先將來源連接的 [IsSourcePathVariable] 選項和目的地連接的 [IsDestinationPatheVariable] 選項設定為 [True]。 接著您就可以選擇要使用的現有系統或使用者自訂變數，或是建立新的變數。 您可以在 [加入變數] 對話方塊中，設定和指定變數的範圍。 此範圍必須是「檔案系統」工作或父容器。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)和[在封裝中使用變數](../Topic/Use%20Variables%20in%20Packages.md)。  
  
> [!NOTE]  
>  若要覆寫您針對 **SourceConnection** 和 **DestinationConnection** 屬性選取的變數，請針對 [來源] 和 [目的地] 屬性輸入運算式。 您可在 [檔案系統工作編輯器] 的 [運算式] 頁面上輸入運算式。 例如，為了設定做為工作目的地使用的檔案路徑，在某些情況下您可能想要使用變數 A，而在其他情況下使用變數 B。  
  
> [!NOTE]  
>  「檔案系統」工作會在單一檔案或目錄上運作。 因此，這項工作不支援使用萬用字元在多個檔案或目錄上執行相同的作業。 為了要讓「檔案系統」工作在多個檔案或目錄上重複作業，請將此「檔案系統」工作放入 Foreach 迴圈容器內。 如需詳細資訊，請參閱[檔案系統工作](../../integration-services/control-flow/file-system-task.md)。  
  
 您可以使用運算式，將不同的變數用於  
  
## 選項。  
 **IsDestinationPathVariable**  
 指出目的地路徑是否儲存在變數中。 這個屬性具有下表中所列的選項。  
  
|Value|說明|  
|-----------|-----------------|  
|**True**|目的地路徑儲存在變數中。 選取這個值會顯示動態選項 [DestinationVariable]。|  
|**False**|目的地路徑是在檔案連接管理員中指定。 選取這個值會顯示動態選項 [DestinationConnection]。|  
  
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
  
|Value|說明|  
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
  
|Value||  
|-----------|-|  
|**True**|目的地路徑儲存在變數中。 選取此值會顯示動態選項 [SourceVariable]。|  
|**False**|目的地路徑是在檔案連接管理員中指定。 選取這個值會顯示動態選項 [DestinationVariable]。|  
  
## IsDestinationPathVariable 動態選項  
  
### IsDestinationPathVariable = True  
 **DestinationVariable**  
 在清單中選取變數名稱，或按一下 [\<新增變數...>] 建立新的變數。  
  
 **相關主題**︰[Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)、[加入變數](../Topic/Add%20Variable.md)  
  
### IsDestinationPathVariable = False  
 **DestinationConnection**  
 在清單中選取檔案連線管理員，或按一下 [\<新增連接...>]，即可建立新的連線管理員。  
  
 **相關主題：** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)、 [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
## IsSourcePathVariable 動態選項  
  
### IsSourcePathVariable = True  
 **SourceVariable**  
 在清單中選取變數名稱，或按一下 [\<新增變數...>] 建立新的變數。  
  
 **相關主題**︰[Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)、[加入變數](../Topic/Add%20Variable.md)  
  
### IsSourcePathVariable = False  
 **SourceConnection**  
 在清單中選取檔案連線管理員，或按一下 [\<新增連接...>]，即可建立新的連線管理員。  
  
 **相關主題：** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)、 [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
## 作業動態選項  
  
### 作業 = 設定屬性  
 **Hidden**  
 指出檔案或目錄是否可見。  
  
 **ReadOnly**  
 指出檔案是否為唯讀。  
  
 **Archive**  
 指出檔案或目錄是否準備就緒，可供封存。  
  
 **系統**  
 指出檔案是否為作業系統檔案。  
  
### 作業 = 建立目錄  
 **UseDirectoryIfExists**  
 指出 [建立目錄] 作業是否會使用具有指定之名稱的現有目錄，而不是建立新的目錄。  
  
## 請參閱＜  
 [Integration Services 錯誤和訊息參考](../../integration-services/integration-services-error-and-message-reference.md)   
 [運算式頁面](../../integration-services/expressions/expressions-page.md)  
  
  