---
title: 簡單 XML 輸入檔範例 (DTA) |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- sample applications [DTA]
ms.assetid: 5b00e4eb-1742-43ec-98d8-d84216b6b840
caps.latest.revision: 21
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: a95a5c086d5c9c941407e6e3a92e2ea4f8cdcd72
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36033802"
---
# <a name="simple-xml-input-file-sample-dta"></a>簡單 XML 輸入檔範例 (DTA)
  請複製用來微調工作負載的這個簡單 XML 輸入檔範例，再將它貼到您喜愛的 XML 編輯器或文字編輯器中。 之後，請利用您的特定微調工作階段的各個值來取代指定給 **Server**、 **Database**、 **Schema**、 **Table**、 **Workload**和 **TuningOptions** 等元素的值。 如需您可以使用這些元素的子項目與屬性的詳細資訊，請參閱[XML 輸入檔參考&#40;Database Engine Tuning Advisor&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)。 下列範例只用到部份可用的屬性及子元素選項。  
  
## <a name="code"></a>程式碼  
 [!code-xml[InputFileSamples#SimpleXMLInputFile](../../snippets/xml/SQL14/dta_xml/inputfilesamples/xml/dta_xml_input_file_samples.xml#simplexmlinputfile)]  
  
## <a name="see-also"></a>另請參閱  
 [啟動及使用 Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)   
 [XML 輸入檔參考 &#40;Database Engine Tuning Advisor&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  