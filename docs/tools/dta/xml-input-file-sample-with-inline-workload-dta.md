---
title: 含內嵌工作負載的 XML 輸入檔範例
titleSuffix: DTA
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: 7c04fe1d-6669-44a1-8b73-36d469e9b002
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: b12c6f285a7c9eb1e32c33332b00ec624092c3c6
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "75258023"
---
# <a name="xml-input-file-sample-with-inline-workload-dta"></a>含內嵌工作負載的 XML 輸入檔範例 (DTA)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

請複製利用 **EventString** 元素指定工作負載的這個 XML 輸入檔範例，再將它貼到您喜愛的 XML 編輯器或文字編輯器中。 您可以利用 **EventString** 元素，在 XML 輸入檔中指定 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼工作負載，而不使用個別的工作負載檔案。 將這個範例複製到編輯工具之後，請利用您的特定微調工作階段的各個值來取代指定給 **Server**、 **Database**、 **Schema**、 **Table**、 **Workload**、 **EventString**和 **TuningOptions** 等元素的值。 如需可以搭配這些元素來使用的所有屬性和子元素的詳細資訊，請參閱 [XML 輸入檔參考 &#40;Database Engine Tuning Advisor&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)。 下列範例只用到部份可用的屬性及子元素選項。

## <a name="code"></a>程式碼

[!code-xml[InputFileSamples#InlineWorkloadInputFile](../../tools/dta/codesnippet/xml/xml-input-file-sample-wi_1.xml)]

## <a name="comments"></a>註解

`USE database_name` EventString **EventString** 陳述式。

## <a name="see-also"></a>另請參閱

- [啟動及使用 Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)
- [檢視及處理 Database Engine Tuning Advisor 的輸出](../../relational-databases/performance/view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md)
- [XML 輸入檔參考XML Input File ReferenceDatabase Engine Tuning Advisor&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)