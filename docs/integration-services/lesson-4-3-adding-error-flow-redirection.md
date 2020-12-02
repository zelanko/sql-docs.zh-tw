---
description: 課程 4-3：新增錯誤流程重新導向
title: 步驟 3：新增錯誤流程重新導向 | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 5683a45d-9e73-4cd5-83ca-fae8b26b488c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: daade3348f7384ed83365923bf94af7b211d6422
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "88457122"
---
# <a name="lesson-4-3-add-error-flow-redirection"></a>課程 4-3：新增錯誤流程重新導向

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



在上一個工作中，當 [查閱貨幣索引鍵] 轉換試圖處理已損毀的範例一般檔案 (會產生錯誤) 時，無法產生相符項目。 因為轉換使用錯誤輸出的預設值，所以任何錯誤都會造成轉換失敗。 當轉換失敗時，封裝的其餘部分也會失敗。  
  
若要不讓轉換失敗，您可以利用錯誤輸出，設定讓元件將失敗的資料列重新導向到另一個處理路徑。 使用個別的錯誤處理路徑可提供更多選項。 例如，您可以清除資料，然後重新處理失敗的資料列。 或者，您可以儲存失敗的資料列及其錯誤資訊，供以後驗證和重新處理。  
  
在此工作中，您會設定 [查閱貨幣索引鍵] 轉換，以將任何失敗的資料列重新導向到錯誤輸出。 在資料流程的錯誤分支中，[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 會將這些資料列寫入檔案。  
  
根據預設，[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 錯誤輸出中的兩個額外資料行 **ErrorCode** 和 **ErrorColumn** 只包含數字錯誤碼，以及發生錯誤之資料行的識別碼。 在此工作中，於套件將失敗的資料列寫入檔案之前，您需使用「指令碼」元件來存取 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] API 及取得該錯誤的描述。  
  
## <a name="configure-an-error-output"></a>設定錯誤輸出  
  
1.  在 **[SSIS 工具箱]** 中，展開 **[通用]** ，然後將 **[指令碼元件]** 拖曳至 **[資料流程]** 索引標籤的設計介面中。將 **[指令碼]** 放到 **[查閱貨幣索引鍵]** 轉換的右邊。  
  
2.  在 [選取指令碼元件類型] 對話方塊中，選取 [轉換]，然後選取 [確定]。  
  
3.  若要連接兩個元件，請選取 [查閱貨幣索引鍵] 轉換，然後將其紅色箭頭拖曳至新的 [指令碼]。  
  
    紅色箭頭代表 **[查閱貨幣索引鍵]** 轉換的錯誤輸出。 藉由使用紅色箭頭將轉換連接到「指令碼」元件，即可將任何處理錯誤重新導向到該「指令碼」元件，然後由它處理這些錯誤並傳送到目的地。  
  
4.  在 [設定錯誤輸出] 對話方塊的 [錯誤] 資料行中，選取 [重新導向資料列]，然後選取 [確定]。  
  
5.  在 [資料流程] 設計介面上，於新的 **ScriptComponent** 中選取 [指令碼元件] 名稱，然後將該名稱變更為 **取得錯誤描述**。  
  
6.  按兩下 [取得錯誤描述] 轉換。  
  
7.  在 **[指令碼轉換編輯器]** 對話方塊的 **[輸入資料行]** 頁面上，選取 **[ErrorCode]** 資料行。  
  
8.  在 [輸入及輸出] 頁面上，展開 [輸出 0]，選取 [輸出資料行]，然後選取 [加入資料行]。  
  
9. 在 [Name] 屬性中，輸入 *ErrorDescription*，然後將 [DataType] 屬性設定為 [Unicode 字串 [DT_WSTR]]。  
  
10. 在 [指令碼] 頁面上，確認 [LocaleID] 屬性是設定為 [英文 (美國)]。
  
11. 選取 [編輯指令碼] 以開啟 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Tools for Applications (VSTA)。 在 **Input0_ProcessInputRow** 方法中，輸入或貼上下列程式碼：  
  
    [Visual Basic]  
  
    ```vb  
    Row.ErrorDescription =   
      Me.ComponentMetaData.GetErrorDescription(Row.ErrorCode)  
    ```  
  
    [Visual C#]  
  
    ```cs
    Row.ErrorDescription = this.ComponentMetaData.GetErrorDescription(Row.ErrorCode);  
    ```  
  
    完成的副程式看起來會像下列程式碼：  
  
    [Visual Basic]  
  
    ```vb
    Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
  
      Row.ErrorDescription =   
        Me.ComponentMetaData.GetErrorDescription(Row.ErrorCode)  
  
    End Sub  
    ```  
  
    [Visual C#]  
  
    ```cs
    public override void Input0_ProcessInputRow(Input0Buffer Row)  
        {  
  
            Row.ErrorDescription = this.ComponentMetaData.GetErrorDescription(Row.ErrorCode);  
  
        }  
    ```  
  
12. 在 [建置] 功能表上，選取 [建置方案] 以建置指令碼並儲存您的變更，然後關閉 VSTA。  
  
13. 選取 [確定] 以關閉 [指令碼轉換編輯器] 對話方塊。  
  
## <a name="go-to-next-task"></a>移至下一個工作
[步驟 4：新增一般檔案目的地](../integration-services/lesson-4-4-adding-a-flat-file-destination.md)  
  
  
  
