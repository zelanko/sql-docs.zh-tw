---
title: 將複製資料行轉換編輯器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.copymaptransformation.f1
helpviewer_keywords:
- Copy Column Transformation Editor
ms.assetid: d8e70541-d563-4ce4-bf66-bc888a0d3026
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 62f2811fb25311ab6aab23d4af66b59befb6611b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48227759"
---
# <a name="copy-column-transformation-editor"></a>複製資料行轉換編輯器
  使用 **[複製資料行轉換編輯器]** 對話方塊，即可選取要複製的資料行，並為新的輸出資料行指派名稱。  
  
 若要深入了解複製資料行轉換，請參閱＜ [Copy Column Transformation](data-flow/transformations/copy-column-transformation.md)＞。  
  
> [!NOTE]  
>  如果只是將所有的來源資料複製到目的地時，就可能不需要使用複製資料行轉換。 在某些不需要進行資料轉換的狀況下，可以將來源直接連接到目的地。 在這些狀況下，最好使用「SQL Server 匯入和匯出精靈」為您建立封裝。 稍後可依需要來增強和重新設定封裝。 如需詳細資訊，請參閱＜ [SQL Server Import and Export Wizard](import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)＞。  
  
## <a name="options"></a>選項。  
 **可用的輸入資料行**  
 使用核取方塊來選取要複製的資料行。 您的選取範圍會將輸入資料行加入下列資料表中。  
  
 **輸入資料行**  
 從可用輸入資料行的清單中選取要複製的資料行。 您的選擇會反映在 **[可用的輸入資料行]** 資料表的核取方塊選擇中。  
  
 **輸出別名**  
 輸入每個新輸出資料行的別名。 預設為 **[的副本]**，後面緊接著輸入資料行的名稱，但是您也可以選擇任何唯一的描述性名稱。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)  
  
  
