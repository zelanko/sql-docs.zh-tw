---
title: 檔案連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- folders [Integration Services], connections
- files [Integration Services], connections
- files [Integration Services]
- connection managers [Integration Services], File
- connections [Integration Services], files
- File connection manager
ms.assetid: 019078bc-44ee-4975-9169-0f9a89e3f3be
caps.latest.revision: 50
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: d9f02969042ec839a708045143b748890d25c1de
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36134468"
---
# <a name="file-connection-manager"></a>檔案連接管理員
  「檔案」連接管理員會啟用封裝以參考現有的檔案或資料夾，或是在執行階段建立檔案或資料夾。 例如，您可以參考 Excel 檔案。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的某些元件會使用檔案中的資訊來執行其工作。 例如，「執行 SQL」工作可參考包含工作執行的 SQL 陳述式之檔案。 有些元件則會對檔案執行作業。 例如，檔案系統工作可參考某個檔案以將其複製到新位置。  
  
## <a name="usage-types-of-the-file-connection-manager"></a>檔案連接管理員的使用類型  
 `FileUsageType`檔案連接管理員的屬性會指定如何使用檔案連接。 「檔案」連接管理員可以建立檔案、建立資料夾、使用現有的檔案，或使用現有的資料夾。  
  
 下表列出的值`FileUsageType`。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|`0`|「檔案」連接管理員會使用現有的檔案。|  
|`1`|「檔案」連接管理員會建立檔案。|  
|`2`|「檔案」連接管理員會使用現有的資料夾。|  
|`3`|「檔案」連接管理員會建立資料夾。|  
  
## <a name="multiple-file-or-folder-connections"></a>多個檔案或資料夾連接  
 「檔案」連接管理員只能參考一個檔案或資料夾。 若要參考多個檔案或資料夾，請使用「多個檔案」連接管理員，而非「檔案」連接管理員。 如需詳細資訊，請參閱 [Multiple Files Connection Manager](multiple-files-connection-manager.md)。  
  
## <a name="configuration-of-the-file-connection-manager"></a>設定檔案連接管理員  
 當您加入檔案連接管理員加入封裝時，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]建立連接管理員會解析為在執行階段的 「 檔案 」 連接、 設定檔案連接屬性，並將 「 檔案 」 連接加入`Connections`封裝的集合。  
  
 `ConnectionManagerType`連接管理員的屬性設定為`FILE`。  
  
 您可以利用下列方式設定「檔案」連接管理員：  
  
-   指定使用類型。  
  
-   指定檔案或資料夾。  
  
 您可以針對檔案連線管理員來設定 ConnectionString 屬性，其方式是在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]的 [屬性] 視窗中指定運算式。 但是，若您在使用運算式來指定檔案或資料夾時想要避免驗證錯誤，請在 **檔案連線管理員編輯器**中針對 **檔案/資料夾**，加入檔案或資料夾的路徑。  
  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計工具中設定之屬性的詳細資訊，請參閱 [File Connection Manager Editor](../file-connection-manager-editor.md)(檔案連線管理員編輯器)。  
  
 如需以程式設計方式設定連接管理員資訊，請參閱<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>和[新增連線以程式設計方式](../building-packages-programmatically/adding-connections-programmatically.md)。  
  
  