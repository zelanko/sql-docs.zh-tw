---
title: 其他檔案 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- files [SQL Server Management Studio], miscellaneous
- projects [SQL Server Management Studio], files
- solutions [SQL Server Management Studio], files
- miscellaneous files folder [SQL Server]
ms.assetid: 3c952b0b-8f5f-4d86-9e5d-616c10b9df0d
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 24a3b22816f33cc204a0809a9f6a38f704baa411
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2019
ms.locfileid: "65105261"
---
# <a name="miscellaneous-files"></a>其他檔案
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
任何專案的外部檔案稱為「其他檔案」(Miscellaneous file)。 您開啟了某個方案之後，便可以開啟和修改關聯於這個專案的其他檔案。 如果副檔名沒有相關的專案程式碼編輯器，這個檔案便會分類為其他檔案。 例如，在 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 指令碼專案中，就會將副檔名為 .txt 或 .mdx 的檔案當作其他檔案來處理。 在 MDX 專案中，副檔名為 .txt 或 .sql 的檔案會當作其他檔案來處理。 若要將副檔名與程式碼編輯器建立關聯，請參閱[如何：使副檔名與程式碼編輯器相關聯](../../relational-databases/scripting/associate-file-extensions-to-a-code-editor.md)。  
  
基於許多原因，能夠將其他檔案加入專案中非常有用。 您可能會有某個檔案不一定是已獲辨識的指令碼，但對於方案的開發而言，卻不可或缺。 常見的範例包括開發附註或指示、資料檔，以及程式碼片段。  
  
其他檔案的運用非常靈活。 例如，假設您有一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 指令碼專案，其中有許多在資料庫中建立資料表和預存程序的指令碼。 另外，您也有許多資料表的資料檔，副檔名為 .BCP，還有在 README.TXT 檔內的執行指示。 您可以將資料和 README 檔當作其他檔案附加至專案，以便利用專案系統的原始檔控制和其他功能。  
  
[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 功能表和工具列會隨著所開啟之檔案的格式而不同。 例如，當您開啟文字檔時，會出現 [文字編輯器] 工具列。 如果您開啟 XML 結構描述檔，便會開啟 [XML 結構描述] 工具列。 當您編輯 XML 結構描述時，無法使用 [文字編輯器] 工具列。 當您在專案檔和其他檔案之間切換時，其他檔案的相關命令和工具列會取代所有專案相關命令和工具列。  
  
## <a name="see-also"></a>另請參閱  
[管理方案和專案的檔案](../../ssms/solution/files-that-manage-solutions-and-projects.md)  
[方案 &#40;SQL Server Management Studio&#41;](../../ssms/solution/solutions-sql-server-management-studio.md)  
[專案 &#40;SQL Server Management Studio&#41;](../../ssms/solution/projects-sql-server-management-studio.md)  
  
