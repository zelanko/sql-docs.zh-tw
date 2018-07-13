---
title: 含內嵌工作負載的 XML 輸入檔案範例 (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- sample applications [DTA]
ms.assetid: 7c04fe1d-6669-44a1-8b73-36d469e9b002
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6e6bdb810dab08a3b46d164389857c1d394b4a20
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37189605"
---
# <a name="xml-input-file-sample-with-inline-workload-dta"></a>含內嵌工作負載的 XML 輸入檔範例 (DTA)
  請複製利用 **EventString** 元素指定工作負載的這個 XML 輸入檔範例，再將它貼到您喜愛的 XML 編輯器或文字編輯器中。 您可以利用 **EventString** 元素，在 XML 輸入檔中指定 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼工作負載，而不使用個別的工作負載檔案。 將這個範例複製到編輯工具之後，請利用您的特定微調工作階段的各個值來取代指定給 **Server**、 **Database**、 **Schema**、 **Table**、 **Workload**、 **EventString**和 **TuningOptions** 等元素的值。 如需所有子項目，您可以使用這些項目與屬性的詳細資訊，請參閱[XML 輸入檔參考&#40;Database Engine Tuning Advisor&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)。 下列範例只用到部份可用的屬性及子元素選項。  
  
## <a name="code"></a>程式碼  
 [!code-xml[InputFileSamples#InlineWorkloadInputFile](../../snippets/xml/SQL14/dta_xml/inputfilesamples/xml/dta_xml_input_file_samples.xml#inlineworkloadinputfile)]  
  
## <a name="comments"></a>註解  
 `USE database_name` EventString **EventString** 陳述式。  
  
## <a name="see-also"></a>另請參閱  
 [啟動及使用 Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)   
 [檢視及處理 Database Engine Tuning Advisor 的輸出](../../relational-databases/performance/view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md)   
 [XML 輸入檔參考 &#40;Database Engine Tuning Advisor&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
