---
title: 建議資料行類型對話方塊 UI 參考 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.suggestdatatypes.f1
ms.assetid: 8d5652e0-cf57-483f-828b-10f00c08418b
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 0fbb0e83bda9f5a7f5b5f10705ef1b770e3205f7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36144769"
---
# <a name="suggest-column-types-dialog-box-ui-reference"></a>建議資料行類型對話方塊 UI 參考
  使用 [建議資料行類型] 對話方塊，根據檔案內容的取樣來識別一般檔案連線管理員中之資料行的資料類型與長度。  
  
 若要深入了解 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 所使用的資料類型，請參閱 [Integration Services 資料類型](../data-flow/integration-services-data-types.md)。  
  
## <a name="options"></a>選項。  
 **資料列數目**  
 輸入或選取演算法所用之範例中的資料列數目。  
  
 **建議最小整數資料類型**  
 清除這個核取方塊以略過評估。 如果選取，則會決定含有整數數值資料之資料行的最小可能整數資料類型。  
  
 **建議最小實數資料類型**  
 清除這個核取方塊以略過評估。 如果選取，則決定含有實數數值資料的資料行是否可使用最小實數資料類型 DT_R4。  
  
 **使用下列的值來識別布林資料行**  
 輸入您要用來作為布林值 True 與 False 的兩個值。 這些值必須以逗號分隔，且第一個值代表 True。  
  
 **填補字串資料行**  
 選取此核取方塊以啟用字串填補。  
  
 **百分比填補**  
 輸入或選取資料行長度的百分比，以用來增加字元資料類型之資料行的長度。 百分比必須是整數。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../integration-services-error-and-message-reference.md)   
 [一般檔案連線管理員](file-connection-manager.md)  
  
  