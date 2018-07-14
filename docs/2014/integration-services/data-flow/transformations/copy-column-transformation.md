---
title: 複製資料行轉換 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.copycolumntrans.f1
helpviewer_keywords:
- columns [Integration Services], copying
- copying columns
- Copy Column transformation
ms.assetid: 1c72a313-9026-46bc-a57f-c6b3f47346f8
caps.latest.revision: 36
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6bd1ef03d1a45151e6f81d46b15e4e7fbc19f9a2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37261464"
---
# <a name="copy-column-transformation"></a>複製資料行轉換
  「複製資料行」轉換會複製輸入資料行，並將新資料行加入轉換輸出，以建立新資料行。 稍後在資料流程中，可將不同的轉換套用至資料行副本。 例如，您可以使用「複製資料行」轉換建立資料行複本，然後使用「字元對應」轉換將複製的資料轉換為大寫字元，或使用「彙總」轉換將彙總套用至新資料行。  
  
## <a name="configuration-of-the-copy-column-transformation"></a>設定複製資料行轉換  
 您可將輸入資料行指定為複製，以設定「複製資料行」轉換。 您可以在一個作業中建立資料行的多份副本，或是建立多個資料行的副本。  
  
 此轉換有一個輸入和一個輸出。 它不支援錯誤輸出。  
  
 您可以透過「 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師」或以程式設計方式設定屬性。  
  
 如需可在 **[複製資料行轉換編輯器]** 對話方塊中設定之屬性的詳細資訊，請參閱＜ [Copy Column Transformation Editor](../../copy-column-transformation-editor.md)＞。  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [通用屬性](../../common-properties.md)  
  
-   [轉換自訂屬性](transformation-custom-properties.md)  
  
 如需如何設定屬性的詳細資訊，請參閱[設定資料流程元件的屬性](../set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="see-also"></a>另請參閱  
 [資料流程](../data-flow.md)   
 [Integration Services 轉換](integration-services-transformations.md)  
  
  
