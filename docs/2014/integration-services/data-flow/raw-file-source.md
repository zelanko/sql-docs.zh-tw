---
title: 原始檔案來源 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.rawfilesource.f1
helpviewer_keywords:
- sources [Integration Services], Raw File
- raw data [Integration Services]
- Raw File source
ms.assetid: 5b4daea5-7f76-4674-aa77-0a79f9f97f7d
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 109880446cf4c30fd3e5cc81e69c768bd8fe94b1
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52805490"
---
# <a name="raw-file-source"></a>原始檔案來源
  「原始檔案」來源會從檔案讀取原始資料。 由於資料的表示法對於來源而言是原生的，因此資料不需翻譯，也幾乎不需要剖析。 這表示，「原始檔案」來源可比其他來源更快讀取資料，例如「一般檔案」和 OLE DB 來源。  
  
 「原始檔案」來源是用來擷取之前由「原始檔案」目的地撰寫的原始資料。 您也可以將原始檔案來源指向僅包含資料行 (僅中繼資料的檔案) 的空白原始檔案。 您可以使用原始檔案目的地產生僅中繼資料的檔案，而不必執行封裝。 如需相關資訊，請參閱 [Raw File Destination](raw-file-destination.md)。  
  
 原始檔案格式包含排序資訊。 原始檔案目的地會儲存所有排序資訊，包括字串資料行的比較旗標。 原始檔案來源會讀取並接受排序資訊。 您可以使用進階編輯器，選擇將原始檔案來源設定為忽略檔案中的排序旗標。 如需比較旗標的詳細資訊，請參閱 [比較字串資料](comparing-string-data.md)。  
  
 您可指定「原始檔案」來源讀取的檔名，藉此設定「原始檔案」。  
  
> [!NOTE]  
>  此來源不會使用連接管理員。  
  
 此來源擁有一個輸出。 它不支援錯誤輸出。  
  
## <a name="configuration-of-the-raw-file-source"></a>設定原始檔案來源  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [Common Properties](../common-properties.md)  
  
-   [原始檔案自訂屬性](raw-file-custom-properties.md)  
  
## <a name="related-tasks"></a>相關工作  
 如需如何設定此元件屬性的資訊，請參閱 [設定資料流程元件的屬性](set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="related-content"></a>相關內容  
  
-   sqlservercentral.com 上的部落格文章： [Raw Files Are Awesome](http://www.sqlservercentral.com/blogs/stratesql/archive/2011/1/1/31-days-of-ssis-_1320_-raw-files-are-awesome-_2800_1_2F00_31_2900_.aspx)(原始檔案太酷了)  
  
## <a name="see-also"></a>另請參閱  
 [Raw File Destination](raw-file-destination.md)   
 [資料流程](data-flow.md)  
  
  
