---
title: 一般檔案來源 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.flatfilesource.f1
- sql13.dts.designer.flatfilesourceadapter.connection.f1
- sql13.dts.designer.flatfilesourceadapter.columns.f1
- sql13.dts.designer.flatfilesourceadapter.errorhandling.f1
helpviewer_keywords:
- sources [Integration Services], Flat File
- text file reading [Integration Services]
- flat files
- Flat File source
ms.assetid: 4a64f7f3-f25d-4db0-93b3-a29496030e58
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f6eea48434554705c49e8291f01a8e32aabfd1b0
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86915002"
---
# <a name="flat-file-source"></a>一般檔案來源

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  「一般檔案」來源會從文字檔讀取資料。 文字檔可以是使用分隔符號、固定寬度或混合的格式。  
  
-   分隔符號格式會使用資料行和資料列分隔符號，來定義資料行和資料列。  
  
-   固定寬度格式會使用寬度來定義資料行和資料列。 此格式亦包含將欄位填補成其最大寬度的字元。  
  
-   不齊右格式會使用寬度來定義所有資料行，最後一個資料行除外，其是以資料列分隔符號所分隔。  
  
 您可以利用下列方式設定「一般檔案」來源：  
  
-   將資料行加入至轉換輸出，該輸出包含「一般檔案」來源從中擷取資料的文字檔檔名。  
  
-   指定「一般檔案」來源是否將資料行中的零長度字串解譯為 Null 值。  
  
    > [!NOTE]  
    >  「一般檔案」來源使用的「一般檔案」連接管理員，必須設定成使用分隔符號格式將零長度字串解譯為 Null。 如果連接管理員使用固定寬度或不齊右格式，則由空格組成的資料就無法解譯為 Null 值。  
  
 一般檔案來源輸出中的輸出資料行包含 FastParse 屬性。 FastParse 可指定資料行要使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 所提供之速度較快，但不區分地區設定的快速剖析常式，或要使用會區分地區設定的標準剖析常式。 如需詳細資訊，請參閱 [快速剖析](https://msdn.microsoft.com/library/6688707d-3c5b-404e-aa2f-e13092ac8d95) 和 [標準剖析](https://msdn.microsoft.com/library/dfe835b1-ea52-4e18-a23a-5188c5b6f013)。  
  
 輸出資料行也包含 UseBinaryFormat 屬性。 您可使用此屬性在檔案中實作二進位資料的支援，例如具有壓縮之十進位格式的資料。 UseBinaryFormat 預設為 [false]  。 如果您想要使用二進位格式，請將 UseBinaryFormat 設為 [true]  ，並將輸出資料行上的資料類型設為 **DT_BYTES**。 當您執行這個動作時，一般檔案來源會略過資料轉換，並將資料直接傳遞到輸出資料行。 然後您就可以使用「衍生的資料行」或「資料轉換」等轉換，將 **DT_BYTES** 資料轉換成不同的資料類型，或者您可以在「指令碼」轉換中撰寫自訂指令碼來解譯資料。 您也可以撰寫自訂的資料流程元件來解譯資料。 如需您可將 **DT_BYTES** 轉換為何種資料類型的詳細資訊，請參閱[轉換 &#40;SSIS 運算式&#41;](../../integration-services/expressions/cast-ssis-expression.md)。  
  
 此來源使用「一般檔案」連接管理員存取文字檔。 藉由設定「一般檔案」連接管理員上的屬性，即可提供有關該檔案及其中各資料行的資訊，以及指定「一般檔案」來源應如何處理文字檔中的資料。 例如，您可以指定分隔檔案中資料行和資料列的字元，以及各資料行的資料類型和長度。 如需相關資訊，請參閱 [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md)。  
  
 此來源有一個輸出和一個錯誤輸出。  
  
## <a name="configuration-of-the-flat-file-source"></a>設定一般檔案來源  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [一般檔案自訂屬性](../../integration-services/data-flow/flat-file-custom-properties.md)  
  
## <a name="related-tasks"></a>相關工作  
 如需如何設定資料流程元件屬性的詳細資訊，請參閱 [Set the Properties of a Data Flow Component](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)(設定資料流程元件的屬性)。  
  
## <a name="flat-file-source-editor-connection-manager-page"></a>一般檔案來源編輯器 (連接管理員頁面)
  使用 **[一般檔案來源編輯器]** 對話方塊的 **[連接管理員]** 頁面，以選取一般檔案來源將要使用的連接管理員。 一般檔案來源會從文字檔讀取資料，其格式可以是分隔、固定寬度或混合格式。  
  
 一般檔案來源可以使用下列其中一種類型的連接管理員：  
  
-   如果來源為單一的一般檔案，則為「一般檔案」連接管理員。 如需相關資訊，請參閱 [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md)。  
  
-   如果來源為多個一般檔案，而且資料流程工作位於迴圈容器 (如 For 迴圈容器) 內，則為「多個一般檔案」連接管理員。 在此容器的每一個迴圈上，「一般檔案」來源會從「多個一般檔案」連接管理員提供的下一個檔案名稱中載入資料。 如需詳細資訊，請參閱 [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)。  
  
### <a name="options"></a>選項。  
 **Flat file connection manager**  
 從清單中選取現有的連線管理員，或按一下 [新增]  建立新的連線管理員。  
  
 **新增**  
 使用 [一般檔案連線管理員編輯器]  對話方塊建立新的連線管理員。  
  
 **將來源的 Null 值保留為資料流程中的 Null 值**  
 指定擷取資料時是否保留 Null 值。 此屬性的預設值為 **false**。 當此值為**alse**時，一般檔案來源會以各資料行適當的預設值取代來源資料的 Null 值，例如字串資料行的空白字串和數值資料行的零。  
  
 **預覽**  
 使用 [資料檢視]  對話方塊來預覽結果。 預覽最多可顯示 200 個資料列。  
  
## <a name="flat-file-source-editor-columns-page"></a>一般檔案來源編輯器 (資料行頁面)
  使用 [一般檔案來源編輯器]  對話方塊的 [資料行]  節點，將輸出資料行對應至每個外部 (來源) 資料行。  
  
> [!NOTE]  
>  在 [一般檔案來源編輯器]  中無法使用一般檔案來源的 **FileNameColumnName** 屬性，以及其輸出資料行的 **FastParse** 屬性，但可使用 [進階編輯器]  來設定這兩個屬性。 如需這些屬性的詳細資訊，請參閱 [一般檔案自訂屬性](../../integration-services/data-flow/flat-file-custom-properties.md)的＜一般檔案來源＞一節。  
  
### <a name="options"></a>選項。  
 **可用的外部資料行**  
 在資料來源中檢視可用的外部資料行清單。 您無法使用此資料表來加入或刪除資料行。  
  
 **[外部資料行]**  
 依工作讀取外部 (來源) 資料行的順序來檢視它們。 首先取消選取資料表中選取的資料行，然後依不同順序從清單中選取外部資料行，就可以變更此順序。  
  
 **輸出資料行**  
 為每個輸出資料行提供唯一的名稱。 預設值為選取的外部 (來源) 資料行的名稱；不過，您也可以選擇任何唯一的、描述性的名稱。 提供的名稱將顯示在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師內。  
  
## <a name="flat-file-source-editor-error-output-page"></a>一般檔案來源編輯器 (錯誤輸出頁面)
  使用 [一般檔案來源編輯器]  對話方塊的 [錯誤輸出]  頁面，以選取錯誤處理選項，並設定錯誤輸出資料行上的屬性。  
  
### <a name="options"></a>選項。  
 **輸入/輸出**  
 檢視資料來源的名稱。  
  
 **資料行**  
 檢視您在 [一般檔案來源編輯器]  對話方塊的 [連線管理員]  頁面上所選取的外部 (來源) 資料行。  
  
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
 [一般檔案目的地](../../integration-services/data-flow/flat-file-destination.md)   
 [資料流程](../../integration-services/data-flow/data-flow.md)  
  
  
