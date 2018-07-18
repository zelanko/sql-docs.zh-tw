---
title: 建議資料行類型對話方塊 UI 參考 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.suggestdatatypes.f1
ms.assetid: 8d5652e0-cf57-483f-828b-10f00c08418b
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2ae4d20627b44b0e0ce71b03b94701b9334b911c
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/12/2018
ms.locfileid: "35409330"
---
# <a name="suggest-column-types-dialog-box-ui-reference"></a>建議資料行類型對話方塊 UI 參考
  使用 [建議資料行類型] 對話方塊，根據檔案內容的取樣來識別一般檔案連線管理員中之資料行的資料類型與長度。  
  
 若要深入了解 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 所使用的資料類型，請參閱 [Integration Services 資料類型](../../integration-services/data-flow/integration-services-data-types.md)。  
  
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
 [Integration Services 錯誤和訊息參考](../../integration-services/integration-services-error-and-message-reference.md)   
 [一般檔案連線管理員](../../integration-services/connection-manager/flat-file-connection-manager.md)  
  
  
