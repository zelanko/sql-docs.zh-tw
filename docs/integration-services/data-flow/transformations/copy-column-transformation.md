---
description: 複製資料行轉換
title: 複製資料行轉換 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.copycolumntrans.f1
- sql13.dts.designer.copymaptransformation.f1
helpviewer_keywords:
- columns [Integration Services], copying
- copying columns
- Copy Column transformation
ms.assetid: 1c72a313-9026-46bc-a57f-c6b3f47346f8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 27673de93d920cdc6adddd12deadcdc4a774d86c
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/19/2020
ms.locfileid: "92194140"
---
# <a name="copy-column-transformation"></a>複製資料行轉換

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  「複製資料行」轉換會複製輸入資料行，並將新資料行加入轉換輸出，以建立新資料行。 稍後在資料流程中，可將不同的轉換套用至資料行副本。 例如，您可以使用「複製資料行」轉換建立資料行複本，然後使用「字元對應」轉換將複製的資料轉換為大寫字元，或使用「彙總」轉換將彙總套用至新資料行。  
  
## <a name="configuration-of-the-copy-column-transformation"></a>設定複製資料行轉換  
 您可將輸入資料行指定為複製，以設定「複製資料行」轉換。 您可以在一個作業中建立資料行的多份副本，或是建立多個資料行的副本。  
  
 此轉換有一個輸入和一個輸出。 它不支援錯誤輸出。  
  
 您可以透過「 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師」或以程式設計方式設定屬性。  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [Common Properties](../set-the-properties-of-a-data-flow-component.md)  
  
-   [轉換自訂屬性](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 如需如何設定屬性的詳細資訊，請參閱 [設定資料流程元件的屬性](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="copy-column-transformation-editor"></a>複製資料行轉換編輯器
  使用 **[複製資料行轉換編輯器]** 對話方塊，即可選取要複製的資料行，並為新的輸出資料行指派名稱。  
  
> [!NOTE]  
>  如果只是將所有的來源資料複製到目的地時，就可能不需要使用複製資料行轉換。 在某些不需要進行資料轉換的狀況下，可以將來源直接連接到目的地。 在這些狀況下，最好使用「SQL Server 匯入和匯出精靈」為您建立封裝。 稍後可依需要來增強和重新設定封裝。 如需詳細資訊，請參閱＜ [SQL Server Import and Export Wizard](~/integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md)＞。  
  
### <a name="options"></a>選項。  
 **可用的輸入資料行**  
 使用核取方塊來選取要複製的資料行。 您的選取範圍會將輸入資料行加入下列資料表中。  
  
 **輸入資料行**  
 從可用輸入資料行的清單中選取要複製的資料行。 您的選擇會反映在 **[可用的輸入資料行]** 資料表的核取方塊選擇中。  
  
 **輸出別名**  
 輸入每個新輸出資料行的別名。 預設為 **[的副本]**，後面緊接著輸入資料行的名稱，但是您也可以選擇任何唯一的描述性名稱。  
  
## <a name="see-also"></a>另請參閱  
 [資料流程](../../../integration-services/data-flow/data-flow.md)   
 [Integration Services 轉換](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
